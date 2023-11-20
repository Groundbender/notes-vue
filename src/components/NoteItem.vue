<template>
  <li class="note" @click="addEditMode">
    <button @click="$emit('delete', note)" class="remove">&times;</button>

    <h2 class="note-title">{{ note.title }}</h2>
    <todo-list :todos="note.todos" />
  </li>
</template>

<script>
import TodoList from "./TodoList.vue";

export default {
  components: {
    TodoList,
  },

  props: {
    note: {
      type: Object,
      required: true,
    },
  },

  methods: {
    addEditMode() {
      this.$emit("edit", this.note);
    },
  },
};
</script>

<style scoped>
.note {
  width: 225px;
  height: 225px;
  background-color: blueviolet;
  padding: 25px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  margin-right: 20px;
  margin-bottom: 20px;
  position: relative;
  overflow: hidden;
  transition: transform 0.2s ease-in-out, background-color 0.2s ease-in-out;
  cursor: pointer;
}

.note:hover {
  transform: scale(1.05);
}
.note:active {
  transform: scale(0.95);
  background-color: lightcoral;
}
.note-title {
  line-height: 1.2;
  font-size: 20px;
  font-weight: bold;
  word-wrap: break-word;
  white-space: normal;
  margin-bottom: 30px;
}

.remove {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: transparent;
  color: rgb(70, 52, 52);
  border: none;
  font-size: 30px;
  cursor: pointer;
  font-weight: 600;
  margin-right: 5px;
  transition: transform 0.2s ease;
}
.remove:hover {
  transform: scale(1.1);
  color: red;
}
.remove:active {
  transform: scale(0.9);
  color: darkred;
}

.note-enter-active {
  transition: transform 0.5s ease, opacity 0.5s ease;
}

.note-enter-from {
  transform: translateY(-20px);
  opacity: 0;
}
</style>
