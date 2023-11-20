<template>
  <form class="note-form" @submit.prevent="createEditNote">
    <label for="input-title" class="input-label">
      Введите заголовок заметки</label
    >
    <input
      id="input-title"
      class="input"
      v-model="note.title"
      @input="title = $event.target.value"
      placeholder="Заголовок"
      required
    />

    <label for="input-todo" class="input-label">
      Введите задачи через запятую</label
    >

    <input
      id="input-todo"
      class="input"
      v-model="todo"
      @input="todo = $event.target.value"
      placeholder="Задача"
      required
    />

    <button class="btn-create" type="submit">
      {{ editMode ? "Редактировать" : " Создать" }}
    </button>
  </form>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  props: {
    editMode: {
      type: Boolean,
      default: false,
    },
    currentNote: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      note: {
        title: (this.currentNote && this.currentNote.title) || "",
        todos: [],
      },
      todo:
        (this.currentNote &&
          this.currentNote.todos.map((todo) => todo.text).join(", ")) ||
        "",
    };
  },
  methods: {
    // универсальная функция для создания и редактирования заметок
    createEditNote() {
      if (!this.note.title || !this.todo) {
        return;
      }
      // если редактирование сохраняем старый id, если создание создаем новый
      if (!this.editMode && !this.currentNote) {
        this.note.id = uuidv4();
      } else {
        this.note.id = this.currentNote.id;
      }

      // не совсем понял по тз как и нужно ли вообще делать добавление тудушек, но решил сделать все-таки таким способом
      const newTodo = this.todo.split(",").map((text) => {
        const trimmedText = text.trim();
        if (trimmedText) {
          return {
            id: uuidv4(),
            text: trimmedText[0].toUpperCase() + trimmedText.slice(1),
            completed: false,
          };
        }
      });
      // убираем falsy значения
      this.note.todos = newTodo.filter(Boolean);
      // эмитим наверх
      this.$emit("create", this.note);

      this.note = {
        title: "",
        todos: [],
      };
      this.todo = "";
    },
  },
};
</script>

<style scoped>
.input {
  width: 100%;
  padding: 10px;
  font-size: 20px;
  border: solid 1px transparent;
  border-radius: 10px;
  margin: 10px;
  transition: border 0.2s ease-in-out;
}
.input:focus {
  outline: none;
  border: solid 1px blueviolet;
}

.note-form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.btn-create {
  padding: 10px 20px;
  font-size: 20px;
  background-color: blueviolet;
  color: white;
  cursor: pointer;
  margin-top: 15px;
  border-radius: 10px;
  transition: transform 0.2s ease-in-out;
  justify-self: left;
}

.input-label {
  align-self: flex-start;
  font-size: 14px;
  font-weight: 500;
}
</style>
