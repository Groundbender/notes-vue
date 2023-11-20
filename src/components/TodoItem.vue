<template>
  <li class="todo-item">
    <span class="todo-item-index">{{ i + 1 }})</span>
    <input id="check" class="todo-checkbox" type="checkbox" disabled />
    <label for="check" class="todo-item-text">{{ todo.text }}</label>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true,
    },
    i: {
      type: Number,
      required: true,
    },
  },
};
</script>

<style scoped>
.todo-item {
  list-style-type: none;
  font-size: 16px;
}
.todo-item-index {
  display: inline-block;
  font-weight: bold;
}
.todo-checkbox {
  opacity: 0;
  visibility: hidden;
}
</style>
