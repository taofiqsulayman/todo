<script>

	import { fade, fly } from 'svelte/transition';
	import { flip } from 'svelte/animate';
	
	let todos = [];
	let inputValue;
	let descValue = "";
	
	const addTodo = () => {
		if (inputValue) {
			let newTodo = {
				title: inputValue,
				description: descValue,
				id: todos.length + 1,
			};
	
			todos = [newTodo, ...todos];
			inputValue = "";
			descValue = "";
		}
	
	}
	
	const deleteTodo = (id) => {
		todos = todos.filter((todo) => todo.id !== id);
	}
	
	</script>
	
	<div class="container">

		<div class="header">
			<h2>TODO LIST</h2>
		</div>

		<form on:submit|preventDefault={addTodo}>
			<label for="title">Todo</label>
			<textarea type="text" bind:value={inputValue} />

			<label for="description">Description</label>
			<textarea type="text" bind:value={descValue} />
			<button on:click={addTodo}>Add</button>
		</form>
	
		{#each todos as todo (todo.id) }
			<div class="todo" animate:flip={{duration:150}} in:fade out:fly={{duration:150}}>
				<h3>{todo.title}</h3>
				<p>{todo.description}</p>
				<button on:click={() => deleteTodo(todo.id)}>X</button>
			</div>
			{:else}
				<h3>Add Some Tasks</h3>
		{/each}
	</div>

	
	<style>

		.header {
			display: flex;
			align-items: center;
			justify-content: center;
			color: #fff;
			padding: 10px 0;
		}

		label {
			color: #fff;
			font-size: large;
		}
	
		.container {
			max-width: 768px;
			margin: 100px auto;
			padding: 0 20px;
		}
	
		form {
			display: flex;
			flex-direction: column;
			justify-content: space-between;
		}
		
		form textarea {
			flex-grow: 1;
			min-width: 80%;
			box-sizing: border-box;
			border-radius: 4px;
			font-size: inherit;
		}
		
		form button {
			border-radius: 4px;
			color: whitesmoke;
			background-color: rgb(7, 156, 106);
			border: 1px solid rgba(0,0,0,0.1);
		}
		
		button {
			padding: 1em;
			border: none;
			box-sizing: border-box;
			font-family: inherit;
			font-size: inherit;
			line-height: 1;
			width: 6em;
		}
	
		.todo {

		background-color: #fff;
    color: #333;
    border-radius: 15px;
    padding: 20px 25px;
    margin: 20px 0;
    position: relative;
		word-wrap: break-word;
		word-break: break-all;

		}
		
		.todo button {
			position: absolute;
			right: -10px;
			top: -10px;
			width: 50px;
			height: 50px;
			background: rgb(203, 24, 78);
			color: #fff;
			border: 1px #eee solid;
			border-radius: 50%;
			padding: 10px;
			text-align: center;
			font-size: 19px;
			cursor: pointer;
		}
		
		.todo button:hover {
			background: rgb(223, 13, 13);
			color: rgb(251, 251, 251);
		}
	</style>