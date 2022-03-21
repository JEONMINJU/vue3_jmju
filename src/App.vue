<template>
	<div>
		<!-- v-show -->
		<!-- <div v-show="toggle">true</div>
		<div v-show="!toggle">false</div> -->

		<!-- v-if -->
		<div v-if="toggle">true</div>
		<div v-else>false</div>

		<button @click="onToggle">Toggle</button>

		<div class="todo__container">
			<h2 class="todo__title">To-Do List</h2>
			<TodoSimpleForm @add-todo="addTodo" />

				<!-- empty 케이스 -->
				<p 
					class="todo__empty"
					v-if="!todos.length"
				>
					추가된 Todo가 없습니다.
				</p>
				
				<TodoList 
					:todos="todos"
					@toggle-todo="toggleTodo"
					@delete-todo="deleteTodo"
				/>
		</div>
	</div>
</template>

<script>
import { ref } from 'vue';
import TodoSimpleForm from './components/TodoSimpleForm.vue';
import TodoList from './components/TodoList.vue';
// import { reactive } from 'vue';

export default {
	components: {
		TodoSimpleForm,
		TodoList,
	},
	setup() {
		const toggle = ref(false);

		const todos = ref([]);
		
		// const todoStyle = {
		// 	textDecoration: 'line-through',
		// 	color: 'gray',
		// }

		const addTodo = (todo) => {
			todos.value.push(todo);

			// if(todo.value === "") {
			// 	hasError.value = true; // error  있다
			// }
			// else {
			// 	todos.value.push({
			// 		id : Date.now(),
			// 		subject: todo.value,
			// 		completed: false,
			// 	});
			// 	hasError.value = false;
			// 	todo.value = '';
			// }

		}

		const onToggle = () => {
			toggle.value = !toggle.value;
		}

		/* list 삭제 */
		const deleteTodo = (index) => {
			todos.value.splice(index, 1);
		}

		return {
			todos,
			addTodo,
			toggle,
			onToggle,
			// todoStyle,
			deleteTodo,
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