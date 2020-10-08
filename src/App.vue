<template>
  <div id="app">
    <div class="todo-wrapper">
      <Header />
      <!-- v-on:하위 컴포넌트에서 발생시킨 이벤트 이름="현재 컴포넌트 메서드 명" -->
      <Input v-on:onAddTodo="handleAddTodo" />
      <List />
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
