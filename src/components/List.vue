<template>
  <section class="main">
    <ul class="todo-list">
      <li v-for="{id, text, isDone} in todos" v-bind:key="id" class="todo">
        <span v-bind:class="{isDone: isDone}" @click="handleToggle(id)">{{
          text
        }}</span>
        <button class="remove-button" type="button" @click="handleButton(id)">
          <img class="remove-icon" src="../assets/delete-icon.svg" />
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
.main {
  width: 100%;
  height: 400px;
  padding: 15px 20px 15px 20px;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  background-color: #fff;
  overflow: scroll;
  -ms-overflow-style: none;
  scrollbar-width: none;
}

.main::-webkit-scrollbar {
  display: none;
}

.main > .todo-list > .todo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 15px 15px 15px;
  margin: 0 0 15px 0;
  border-bottom: 1px solid grey;
}

.main > .todo-list > .todo > span {
  max-width: 300px;
  line-height: 15px;
}

.main > .todo-list > .todo > .remove-button {
  position: relative;
  width: 20px;
  height: 20px;
}

.main > .todo-list > .todo > .remove-button > .remove-icon {
  width: 100%;
  height: 100%;
  cursor: pointer;
}

.main > .todo-list > .todo:last-child {
  margin: 0 0 0 0;
}

.isDone {
  text-decoration-line: line-through;
}
</style>
