<template>
  <section class="main">
    <ul class="todo-list">
      <li v-for="{ id, text } in todos" :key="id">
        {{ text }}
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
  },
};
</script>

<style scoped>
</style>