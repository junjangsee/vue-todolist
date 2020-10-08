<template>
  <div id="app">
    <div class="todo-wrapper">
      <Header />
      <Input />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import Input from "./components/Input";

export default {
  name: "App",
  components: {
    Header,
    Input,
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
