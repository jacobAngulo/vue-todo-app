<template>
  <div>
    <form v-on:submit="addTodo">
      <input type="text" v-model="title" name="title" placeholder="Add Todo...">
      <input type="submit" value="Submit ">
    </form>
  </div>
</template>

<script>
export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        title: this.title,
        completed: false
      };
      // send up to paent where data is at
      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>

<style  >
</style>