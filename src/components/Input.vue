<template>
  <input
    type="text"
    v-model="text"
    class="input-todo"
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

<style scoped>
.input-todo {
  width: 100%;
  height: 40px;
  padding: 0 15px 0 15px;
  margin: 0 0 30px 0;
  border-radius: 4px;
  letter-spacing: 2px;
  box-shadow: 5px 5px 20px #489dcf;
}
.input-todo::-webkit-input-placeholder {
  font-size: 15px;
}
.input-todo::-ms-input-placeholder {
  font-size: 15px;
}
</style>
