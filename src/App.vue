<template>
  <div id="app">
    <div class="todo-wrapper">
      <Header />
      <Input v-on:onAddTodo="handleAddTodo" />
      <List v-bind:todos="todos" v-on:onRemoveTodo="handleRemoveTodo" />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import Input from "./components/Input";
import List from "./components/List";

export default {
  name: "App",
  components: {
    Header,
    Input,
    List,
  },

  data() {
    return {
      todos: [],
    };
  },

  created() {
    if (localStorage.length !== 0) {
      for (let i = 0; i < localStorage.length; i += 1) {
        if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
          this.todos = [
            ...this.todos,
            JSON.parse(localStorage.getItem(localStorage.key(i))),
          ];
        }
      }
    }
  },

  methods: {
    handleAddTodo(title) {
      const todo = {
        id: new Date().getTime(),
        text: title,
        isDone: false,
      };

      localStorage.setItem(todo.id, JSON.stringify(todo));
      this.todos = [...this.todos, todo];
    },

    handleRemoveTodo(todoId) {
      localStorage.removeItem(todoId);
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
