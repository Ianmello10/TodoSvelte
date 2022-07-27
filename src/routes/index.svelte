<script>
	import { each } from 'svelte/internal';
	import '../app.css';
	import Addimg from '../image/add-outline.svg';
	import Trashimg from '../image/trash-outline.svg';

	export let tasks = [];
	let msg = '';
	let title = "";

	function addTask() {  
		 
		  if(msg === "")return alert("invalid")
		
		let _id = Date.now() * Math.random();
		 
		tasks = tasks.concat({ id: _id, check:false, text: msg , titleTodo:title }); 
		msg =  "" ;
	}

	function deleteTask(id) {
		tasks = tasks.filter((element) => element.id !== id);
	}

	function activeTask() {
		if (tasks.check !== true) {
			tasks.check = true;
			this.classList.add('border-l-4');
		} else {
			tasks.check = false;
			this.classList.remove('border-l-4');
		}
	}
</script>

<div class="w-full">
	<div class="w-[30%] mx-auto mt-28 bg-[#F3F1F5] rounded-md  h-auto pb-6 flex flex-col gap-y-2 ">
		<div class="w-[90%] mx-auto text-2xl h-10 mt-6">
			<h1 class="font-bold">TodoApp</h1>
		</div>

		<div class="w-[90%] mx-auto flex justify-between items-center  h-14 ">
			<input
				bind:value={msg}
				id="input"
				class="w-[80%] h-10 border-2 px-2 rounded- outline-0"
				type="text"
				placeholder="digite uma tarefa"
			/>

			<div
				on:click={addTask}
				id="addTask"
				class="w-12 h-10 bg-[#BFA2DB] cursor-pointer rounded-sm flex items-center justify-around "
			>
				<div class="w-10 "><img class="w-full" src={Addimg} alt="" /></div>
			</div>
		</div>

		<div id="container-task" class="w-[90%] mx-auto h-auto flex flex-col gap-y-2">
			<div
				class="w-full h-10 border-l-4   border-[#a181be]   rounded-sm px-2 bg-[#F0D9FF] flex justify-between items-center "
			>
				<p class="text-black ">Task exemplo</p>

				<img
					class="w-6 cursor-pointer transition-transform ease-out duration-150 hover:-translate-y-1"
					src={Trashimg}
					alt=""
				/>
			</div>

			{#each tasks as task}
				<div
					on:click={activeTask}
					class="w-full h-10  border-[#a181be]  justify-between  rounded-sm px-2 bg-[#F0D9FF] flex items-center cursor-pointer"
				>
					<p class="text-black " id="out">{task.text}</p>

					<img
						on:click={deleteTask(task.id)}
						class="w-6 cursor-pointer transition-transform ease-out duration-150 hover:-translate-y-1"
						src={Trashimg}
						alt=""
					/>
				</div>
			{/each}

			<div class="mt-5">Total de Tarefas : {tasks.length} </div>
		</div> 

	</div>
</div>
