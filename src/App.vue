<template>
  <div id="app">
    <div class="todo-wrapper">
      <Header />
      <Input v-on:onAddTodo="handleAddTodo" />
      <List
        v-bind:todos="filtedTodos"
        v-on:onRemoveTodo="handleRemoveTodo"
        v-on:onToggleTodo="handleToggleTodo"
      />
      <Footer
        v-bind:filterType="filterType"
        v-bind:size="filtedTodos.length"
        v-on:onFilterType="handleFilterType"
        v-on:onClearTodo="handleClearTodo"
      />
    </div>
  </div>
</template>

<script>
import "./assets/css/reset.css";

import Header from "./components/Header";
import Input from "./components/Input";
import List from "./components/List";
import Footer from "./components/Footer";

export default {
  name: "App",
  components: {
    Header,
    Input,
    List,
    Footer,
  },

  data() {
    return {
      todos: [],
      filterType: "ALL",
    };
  },

  computed: {
    filtedTodos() {
      switch (this.filterType) {
        case "ALL": {
          return this.todos;
        }
        case "DOING": {
          return this.todos.filter((todo) => todo.isDone === false);
        }
        case "DONE": {
          return this.todos.filter((todo) => todo.isDone === true);
        }
        default:
          return [];
      }
    },
  },

  created() {
    this.todos = JSON.parse(localStorage.getItem("todos")) || [];
  },

  methods: {
    handleAddTodo(title) {
      const todo = {
        id: new Date().getTime(),
        text: title,
        isDone: false,
      };

      const newTodo = [...this.todos, todo];
      localStorage.setItem("todos", JSON.stringify(newTodo));
      this.todos = newTodo;
    },

    handleRemoveTodo(todoId) {
      const currentTodos = [...this.todos];
      const removedTodos = currentTodos.filter((todo) => todo.id !== todoId);

      this.todos = removedTodos;

      localStorage.clear();
      localStorage.setItem("todos", JSON.stringify(removedTodos));
    },

    handleToggleTodo(todoId) {
      const currentTodos = [...this.todos];
      const todo = currentTodos.find((todo) => todo.id === todoId);

      if (!todo) return;

      todo.isDone = !todo.isDone;
      const toggledTodos = currentTodos;
      this.todos = toggledTodos;

      localStorage.clear();
      localStorage.setItem("todos", JSON.stringify(toggledTodos));
    },

    handleFilterType(filterType) {
      this.filterType = filterType;
    },

    handleClearTodo() {
      this.todos = [];
      localStorage.clear();
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #56bdfb;
}

.todo-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 400px;
  height: 600px;
}
</style>
