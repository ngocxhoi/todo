<template>
  <form @submit.prevent="submit">
    <input required type="text" placeholder="Todo" v-model="title" />
    <input required type="text" placeholder="Description" v-model="desc" />
    <button style="cursor: pointer" type="submit">Save</button>
  </form>
</template>

<script setup>
const emits = defineEmits(["onEditTodo"]);
const props = defineProps({
  todoEdit: {
    type: Object,
    default: {
      title: "",
      desc: "",
    },
  },
});
const { todoEdit } = toRefs(props);

let title = ref();
let desc = ref();

onMounted(() => {
  title.value = todoEdit.value.title;
  desc.value = todoEdit.value.desc;
});

function emitEditTodo() {
  emits("onEditTodo", {
    title: title.value,
    desc: desc.value,
  });
}
function submit() {
  emitEditTodo();
}
</script>

<style></style>
