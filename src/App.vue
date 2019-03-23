<template>
  <div id="app">
    <Header/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
    <AddTodo v-on:add-todo="addTodo"/>
    <button v-on:click="clearCompleted">clear completed</button>
  </div>
</template>


<script>
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
import Header from "./components/layout/Header";

export default {
  name: "app",
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "todo 1",
          completed: false
        },
        {
          id: 2,
          title: "todo 2",
          completed: true
        },
        {
          id: 3,
          title: "todo 3",
          completed: false
        }
      ]
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => {
        return todo.id !== id;
      });
    },

    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => {
        return todo.completed === false;
      });
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
