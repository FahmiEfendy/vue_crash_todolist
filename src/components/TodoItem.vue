<template>
  <!-- Binding class 'is-complete' if todo.completed = true -->
  <div class="todo-item" v-bind:class="{ 'is-complete': todo.completed }">
    <p>
      <!-- Trigger markComplete() everytime checkbox toggled -->
      <input type="checkbox" v-on:change="markComplete" />
      {{ todo.title }}
      <!-- Emit (send to Todos.vue (parent)) an event del-todo to send todo.id as a payload -->
      <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  // Accessing props made with (v-bind:todo="todo") from Todos.vue
  props: ["todo"],
  data() {
    return {
      // Saving todo (index todos) as local data to prevent mutating a prop
      todoLocal: this.todo,
    };
  },
  methods: {
    markComplete() {
      // Turn false to true or true to false
      this.todoLocal.completed = !this.todoLocal.completed;
    },
  },
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>