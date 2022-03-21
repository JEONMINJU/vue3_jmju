<template>
	<div>
			<form 
				v-on:submit="onSubmit"
				class="todo__form"
			>
			<div>
			<input
					type="text"
					class="todo__input"
					v-model="todo"
					placeholder="Type new to-do"
				>
				<button
					type="submit"
					class="todo__btn"
					@click="onSubmit"
				>
					Add
				</button>
			</div>
			
			<!-- display:none/block -->
			<div v-show="hasError">This field cannot be empty</div>
			</form>
	</div>
</template>

<script>
	import { ref } from 'vue';

	export default {
		setup(props, context) {
			const todo = ref("");
			const hasError = ref(false);

			const onSubmit = (e) => {
				e.preventDefault();
				
				if(todo.value === "") {
					hasError.value = true; // error  있다
				}
				else {
					context.emit('add-todo', {
						id: Date.now(),
						subject: todo.value,
						completed: false,
					})
					// todos.valu e.push({
					// 	id : Date.now(),
					// 	subject: todo.value,
					// 	completed: false,
					// });
					hasError.value = false;
					todo.value = '';
				}
			};

			return {
				todo,
				hasError,
				onSubmit,
			}
		}
	}
</script>

<style lang="scss" scoped>
	.todo {
		&__container {
			width: 400px;
			height: 500px;
			border: 1px solid #eee;
		}

		&__title {
			text-align: center;
		}

		&__form {
			text-align: center;
		}

		&__input {
			width: 300px;
			height: 20px;
			margin-right: 10px;
		}

		&__btn {
			width: 60px;
			height: 28px;
			background: rgb(181, 209, 209);
			border: none;
			border-radius: 10px;
			cursor: pointer;
		}

		&__empty {
			width: 370px;
			height: 300px;
			
			text-align: center;
			line-height: 300px;
		}

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