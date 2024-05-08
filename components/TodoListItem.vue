<template>
  <div v-if="!todo.editMode">
    <input type="checkbox" :value="todo.isChecked" @click="emitCheck">
    <p class="tooltip">
      <strong>{{ todo.title }}</strong>
      <p class="tooltiptext">
        <span>{{ todo.desc }}</span>
      </p>
    </p>

    <button @click="toggleEditTodo">Edit</button>
    <button @click="onDeleteTodo">Delete</button>
  </div>

  <div v-else>
    <EditForm :todoEdit="todo" @onEditTodo="onEditTodo"/>
  </div>
</template>

<script setup>
const props = defineProps(["todo", 'indexTodoList']);
const emits = defineEmits(['checkBox', 'toggleEditTodo', 'onEditTodo', 'onDeleteTodo']);
const { todo, indexTodoList } = toRefs(props);

function emitCheck() {
  emits('checkBox', indexTodoList.value);
}

function toggleEditTodo() {
  emits('toggleEditTodo', indexTodoList.value);
}

function onEditTodo(e) {
  emits('onEditTodo', {editTodo: {
    ...e
  }, indexTodoList: indexTodoList.value});

  toggleEditTodo();
}

function onDeleteTodo() {
  emits('onDeleteTodo', indexTodoList.value);
}
</script>

<style></style>
