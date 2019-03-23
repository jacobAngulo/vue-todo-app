<template>
  <div id="app">
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
    <AddTodo v-on:add-todo="addTodo"/>
    <button v-on:click="clearCompleted">clear completed</button>
  </div>
</template>


<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: "app",
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    async deleteTodo(id) {
      try {
        const deleted = await axios.delete(
          `https://jsonplaceholder.typicode.com/todos/${id}`
        );
        this.todos = this.todos.filter(todo => {
          return todo.id !== id;
        });
      } catch (error) {
        console.log(error);
      }
    },

    async addTodo(newTodo) {
      const { title, completed } = newTodo;
      try {
        const posted = await axios.post(
          "https://jsonplaceholder.typicode.com/todos",
          { title, completed }
        );
        this.todos = [...this.todos, posted.data];
      } catch (error) {
        console.log(error);
      }
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => {
        return todo.completed === false;
      });
    }
  },
  async created() {
    try {
      const todos = await axios.get(
        "https://jsonplaceholder.typicode.com/todos?_limit=10`"
      );
      this.todos = todos.data;
      console.log(todos.data);
    } catch (error) {
      console.log(error);
    }
  }
};
</script>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
