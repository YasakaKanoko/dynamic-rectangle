<script setup>
import { ref } from 'vue';
const todos = ref([
  { item: "Vue", isComplete: false },
  { item: "React", isComplete: false },
  { item: "Nuxt", isComplete: false },
  { item: "Next", isComplete: false },
  { item: "Node", isComplete: false },
  { item: "Nest", isComplete: false },
  { item: "React Native", isComplete: false },
  { item: "Electron", isComplete: false },
  { item: "Rust", isComplete: false }]
);
const curTodo = ref("");
const addTodo = () => {
  if (!curTodo.value.trim().length) {
    console.log('The input is Empty!')
    return;
  }
  todos.value.push({ item: curTodo.value, isComplete: false });
  curTodo.value = "";
}
const delTodo = (removeTodo) => {
  return todos.value = todos.value.filter((todo) => todo.item !== removeTodo.item);
}
const completeItem = (item) => {
  const index = todos.value.findIndex((todo) => todo.item === item.item);
  todos.value[index] = { ...todos.value[index], isComplete: true };
}
</script>

<template>
  <h1>Todo List</h1>
  <input type="text" placeholder="Enter your todo you want to add" v-model="curTodo" />
  <button @click="addTodo">Add</button>
  <hr>
  <ul v-for="(todo, idx) in todos">
    <li :key="idx">
      <div :class="todo.isComplete ? 'complete' : ''">{{ todo.item }}</div>
      <button v-if="!todo.isComplete" @click="completeItem(todo)">Complete</button>
      <button @click="delTodo(todo)">&times;</button>
    </li>
  </ul>
</template>

<style scoped>
button {
  margin: 0 3px;
}

.complete {
  text-decoration: line-through;
}

div {
  display: inline-block;
}
</style>
