<template>
  <div id="app">
    <h1>TODO APP</h1>
    <TodoForm @onNewTodo="handleNewTodo" />
    <div v-if="todoList">
      <div
        v-for="(todo, index) in todoList"
        :key="index"
        style="border-bottom: 1px solid black"
      >
        <TodoListItem
          :todo="todo"
          :indexTodoList="index"
          @checkBox="handleCheckBox"
          @toggleEditTodo="handleToggleTodo"
          @onEditTodo="handleEditTodo"
          @onDeleteTodo="handleDeleteTodo"
        />
      </div>
    </div>
  </div>
</template>

<script setup>
let todoList = ref([]);

function handleNewTodo(newTodo) {
  todoList.value.push(newTodo);
}

function handleCheckBox(indexTodoList) {
  let todo = todoList.value[indexTodoList];
  todo.isChecked = !todo.isChecked;
}

function handleToggleTodo(indexTodoList) {
  let todo = todoList.value[indexTodoList];
  todo.editMode = !todo.editMode;
}

function handleEditTodo(data) {
  let todo = todoList.value[data.indexTodoList];
  todo.title = data.editTodo.title;
  todo.desc = data.editTodo.desc;
}

function handleDeleteTodo(indexTodoList) {
  let todo = todoList.value[indexTodoList];
  if (todo.isChecked && confirm("Are you sure you want to delete"))
    todoList.value.splice(indexTodoList, 1);
  else {
    if (!todo.isChecked) alert("Please done this action yet");
  }
}
</script>

<style>
/* Tooltip container */
.tooltip {
  position: relative;
  display: inline-block;
  border-bottom: 1px dotted black; /* If you want dots under the hoverable text */
}

/* Tooltip text */
.tooltip .tooltiptext {
  visibility: hidden;
  width: 120px;
  background-color: black;
  color: #fff;
  text-align: center;
  padding: 5px 0;
  border-radius: 6px;

  /* Position the tooltip text - see examples below! */
  position: absolute;
  z-index: 1;
}

/* Show the tooltip text when you mouse over the tooltip container */
.tooltip:hover .tooltiptext {
  visibility: visible;
}
</style>
