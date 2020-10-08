<template>
  <section class="main">
    <ul class="todo-list">
      <li v-for="{ id, text } in todos" :key="id">{{ text }}</li>
    </ul>
  </section>
</template>

<script>
export default {
  props: ["todos"],
  methods: {},
};
</script>

<style scoped>
</style>