<template>
  <div>
    <!-- Accessing every index (with todo) in todos (todoArray)
         Binding todo.id to key -->
    <div v-for="todo in todos" v-bind:key="todo.id">
      <!-- Binding each index "todo" to todo 
           If del-todo triggered, emit todo.id that get from Todoitem.vue to App.vue -->
      <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  // Component name should be multi word
  name: "TodosWord",
  // Access component TodoItem from TodoItem.vue
  components: {
    TodoItem,
  },
  // Accessing props todos made with (v-bind:todos="todoArray") from HomeView.vue
  props: ["todos"],
};
</script>

<style scoped>
</style>