<script lang="ts">
	import Input from './Input.svelte'
	import { derived, writable } from 'svelte/store'

	let todoName = ""
	const todosList = writable([])

	const handleChange = (newValue:string) => todoName = newValue;

	const addNewTodo = () => {
		const newTodo = {name:todoName, id: Math.random() * 1000}
		todosList.update(todos => [...todos, newTodo])
		todoName = ""
	}

	const todos = derived(todosList, $todosList => $todosList)
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>Todo list</h1>

	<p>New todo name: {todoName}</p>
	<Input handleChange={handleChange} placeholder="Clean up your code" />

	<button on:click={addNewTodo}>Add Todo</button>

	{#if $todos.length > 0}
	<p>List of todos:</p>

	{#each $todos as todo, index(todo.id)}
	<p>{index}: {todo.name}</p>
	{/each}
	{:else}
	<p>No todos to do</p>
	{/if}
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}
</style>
