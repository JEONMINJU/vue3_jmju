<!-- class 바인딩 -->
<div :class="{ active: isActive }"></div>
isActive 가 true 면 active 라는 클래스를 넣어준다.

<label
	class="todo__label"
	:class="{ todo__done: todo.completed }"
>
	{{ todo.subject }}
</label>

<!-- style 바인딩 -->
<label
	class="todo__label"
	:style="todo.completed ? todoStyle : {}"
>
	{{ todo.subject }}
</label>


부모에서 자식으로 보내는게 props