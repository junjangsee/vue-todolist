<template>
  <footer class="footer">
    <span class="todo-count">
      <strong>{{ size }}</strong> items left
    </span>
    <ul class="filter-list">
      <li v-for="(filter, idx) in filters" v-bind:key="idx">
        <button
          v-bind:class="{selected: filterType === filter}"
          @click="handleFilterType(filter)"
          type="button"
        >
          {{ filter }}
        </button>
      </li>
      <li>
        <button class="clear-todo" type="button">Clear Todo</button>
      </li>
    </ul>
  </footer>
</template>

<script>
export default {
  props: ["filterType", "size"],
  data() {
    return {
      filters: ["ALL", "DOING", "DONE"],
    };
  },

  methods: {
    handleFilterType(type) {
      this.$emit("onFilterType", type);
    },
  },
};
</script>

<style scoped></style>
