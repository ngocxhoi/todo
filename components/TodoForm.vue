<template>
  <form @submit.prevent="submit">
    <input required type="text" placeholder="Todo" v-model="title" />
    <input required type="text" placeholder="Description" v-model="desc" />
    <button style="cursor: pointer" type="submit">Add</button>
  </form>
</template>

<script setup>
const emits = defineEmits(["onNewTodo"]);

let title = ref();
let desc = ref();

function emitNewTodo() {
  emits("onNewTodo", {
    title: title.value,
    desc: desc.value,
    isChecked: false,
    editMode: false,
  });
}
function submit() {
  emitNewTodo();
  title.value = "";
  desc.value = "";
}
</script>

<style></style>
