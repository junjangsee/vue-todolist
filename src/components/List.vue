<template>
  <section class="main">
    <ul class="todo-list">
      <li v-for="{ id, text, isDone } in todos" v-bind:key="id">
        <span v-bind:class="{ isDone: isDone }" @click="handleToggle(id)">{{
          text
        }}</span>
        <button class="remove-button" type="button" @click="handleButton(id)">
          삭제
        </button>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  props: ["todos"],
  methods: {
    handleButton(todoId) {
      this.$emit("onRemoveTodo", todoId);
    },

    handleToggle(todoId) {
      this.$emit("onToggleTodo", todoId);
    },
  },
};
</script>

<style scoped>
.isDone {
  text-decoration-line: line-through;
}
</style>