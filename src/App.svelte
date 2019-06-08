<script>
	let newTodo = ''
	let todos = [{
		description: 'example todo item',
		completed: false
	}]

	const updateTodo = (event) => {
		newTodo = event.target.value
	}

	const addTodo = () => {
		todos = [...todos, {description: newTodo, completed: false}]
		newTodo = null
	}

	const removeTodo = (index) => {
		todos = todos.filter((todo, idx) => idx !== index)
	}
	
	const handleCheck = (index) => {
		todos = todos.map((todo, idx) => {
			return idx === index ? {...todo, completed: !todo.completed} : todo
		})
	}
</script>

<style>
	h1 {
		color: purple;
	}
	.button-remove {
		margin-left: 10px;
	}
	.checked {
		text-decoration: line-through;
	}
</style>

<h1>Todo's</h1>
<ul>
	{ #each todos as todo, index }
		<li>
			<span class={ todo.completed ? 'checked' : '' } on:click={ () => handleCheck(index) }>{ todo.description }</span>
			<button class='button-remove' type='button' on:click={ () => removeTodo(index) }>x</button>
		</li>
	{ /each }
</ul>

<input type='text' on:change={ updateTodo} value={ newTodo }/>
<button type='button' on:click={ addTodo }>Add</button>
