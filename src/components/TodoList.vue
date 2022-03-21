<template>
<div>
	<ul 
		v-for="(todo, index) in todos"
		:key="todo.id"
		class="todo__card"
	>
			<li class="todo__card__list">
				<input 
					type="checkbox"
					class="todo__check"
					v-model="todo.completed"
				>
				<label
					class="todo__label"
					:class="{ todo__done: todo.completed }"
				>
					{{ todo.subject }}
				</label>

				<button 
					type="button"
					class="todo__delete"
					@click="deleteTodo(index)"
				>
					Delete
				</button>
			</li>
	</ul>
</div>
</template>

<script>
export default {
		props: ['todos'], // props로 todos를 받아오는구나

		setup(props, context) {
			const toggleTodo = (index) => {
				context.emit('toggle-todo', index);
			};

			const deleteTodo = (index) => {
				context.emit('delete-todo', index);
			};

			return {
				toggleTodo,
				deleteTodo,
			}
		}
}
</script>

<style lang="scss" scoped>
	.todo {
		&__card {
			padding: 0;

			&__list {
				margin: 5px;
				padding: 10px;
				border: 1px solid #eaeaea;
				list-style: none;
			}
		}

		&__done {
			text-decoration: line-through;
		}

		&__delete {
			margin-left: 30px;
		}
	}
</style>