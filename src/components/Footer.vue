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
        <button class="clear-todo" type="button" @click="handleClear">
          CLEAR
        </button>
      </li>
    </ul>
  </footer>
</template>

<script>
export default {
  props: ["filterType", "size", "handleClearTodo"],
  data() {
    return {
      filters: ["ALL", "DOING", "DONE"],
    };
  },

  methods: {
    handleFilterType(type) {
      this.$emit("onFilterType", type);
    },

    handleClear() {
      this.$emit("onClearTodo");
    },
  },
};
</script>

<style scoped>
.footer {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  height: 59px;
  border-top: 1px solid #8e8e8e;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
  background-color: #fff;
}

.footer > .todo-count {
  margin: 3px 0 3px 0;
}

.footer > .filter-list {
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 100%;
  height: 100%;
}

.footer > .filter-list > li {
  padding: 4px;
}

.footer > .filter-list > li > button {
  cursor: pointer;
  font-size: 14px;
}

.footer > .filter-list > li > .selected {
  color: coral;
  font-weight: 700;
}

.footer > .filter-list > li > .clear-todo:hover {
  color: red;
}
</style>
