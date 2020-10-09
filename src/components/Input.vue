<template>
  <input
    type="text"
    v-model="text"
    class="new-todo"
    placeholder="Write Your Todo..."
    autofocus
    autocomplete="off"
    v-on:keypress.enter="handleInput"
  />
</template>

<script>
export default {
  data() {
    return {
      text: "",
    };
  },
  methods: {
    handleInput() {
      if (this.text === "") return;

      this.$emit("onAddTodo", this.text);
      this.text = "";
    },
  },
};
</script>

<style scoped></style>
