<template>
  <div id="app">
    <div class="todo-wrapper">
      <Header />
      <Input v-on:onAddTodo="handleAddTodo" />
      <List
        v-bind:todos="filterTodos"
        v-on:onRemoveTodo="handleRemoveTodo"
        v-on:onToggleTodo="handleToggleTodo"
      />
      <Footer
        v-bind:filterType="filterType"
        v-bind:size="filterTodos.length"
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
    filterTodos() {
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
    if (localStorage.length === 0) return;

    for (let i = 0; i < localStorage.length; i += 1) {
      if (localStorage.key(i) !== "loglevel:webpack-dev-server") {
        this.todos = [
          ...this.todos,
          JSON.parse(localStorage.getItem(localStorage.key(i))),
        ];
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

    handleToggleTodo(todoId) {
      const currentTodos = [...this.todos];
      const todo = currentTodos.find((todo) => todo.id === todoId);

      if (todo) {
        todo.isDone = !todo.isDone;
        this.todos = currentTodos;
      }

      localStorage.removeItem(todoId);
      localStorage.setItem(todo.id, JSON.stringify(todo));
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
  justify-content: center;
  align-items: center;
  width: 400px;
  height: 600px;
}
</style>
