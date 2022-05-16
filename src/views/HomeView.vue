<template>
  <div id="home">
    <!-- Access emit add-todo from AddTodo.vue and trigger addTodo -->
    <AddTodo v-on:add-todo="addTodo" />
    <!-- Binding todoArry to todos
         Access emit del-todo from Todoitem.vue and trigger deleteTodo -->
    <TodosWord v-bind:todos="todoArray" v-on:del-todo="deleteTodo($event)" />
  </div>
</template>

<script>
import TodosWord from "../components/Todos";
import AddTodo from "../components/AddTodo";
// Axios used for applying promised HTTP
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    TodosWord,
    AddTodo,
  },
  data() {
    return {
      // Array to store TodoList
      todoArray: [],
    };
  },
  methods: {
    // id used to take a todo.id delivered by payload from TodoItem.vue -> Todos.vue -> HomeView.vue
    deleteTodo(id) {
      axios
        .delete("https://jsonplaceholder.typicode.com/todos/${id}")
        // Filtering todo that doesnt have same id that was taken by payload
        .then(
          (res) =>
            (this.todoArray = this.todoArray.filter(
              (todoArray) => todoArray.id !== id
            ))
        )
        .catch((err) => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed,
        })
        // Put in data to todoArray
        .then((res) => (this.todoArray = [...this.todoArray, res.data]))
        .catch((err) => console.log(err));
    },
  },
  created() {
    axios
      // Take todolist from todos jsonplaceholder and limiting only 5 todo
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => (this.todoArray = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>