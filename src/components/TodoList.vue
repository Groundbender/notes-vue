<template>
  <ul class="todo-list">
    <todo-item
      v-for="(todo, i) in todos.slice(0, 4)"
      :key="todo.id"
      :todo="todo"
      :i="i"
    />
  </ul>
</template>
<script>
import TodoItem from "./TodoItem.vue";
export default {
  components: {
    TodoItem,
  },
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.todo-list {
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
