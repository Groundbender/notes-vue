<template>
  <main>
    <modal
      v-model:show="modalVisible"
      v-model:currentNote="currentNote"
      v-model:editMode="editMode"
    >
      <note-form
        @create="createEditNote"
        :editMode="editMode"
        :currentNote="currentNote"
      />
    </modal>

    <div class="container">
      <my-header @open="showModal"></my-header>
      <note-list
        v-if="notes.length > 0"
        @edit="addEditMode"
        :notes="notes"
        @delete="deleteNote"
      />

      <empty-notes v-else></empty-notes>
    </div>
  </main>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

import NoteForm from "./components/NoteForm.vue";
import NoteList from "./components/NoteList.vue";
import Modal from "./components/UI/Modal.vue";
import MyHeader from "./components/MyHeader.vue";
import EmptyNotes from "./components/EmptyNotes.vue";
export default {
  components: {
    NoteForm,
    NoteList,
    Modal,
    MyHeader,
    EmptyNotes,
  },
  data() {
    return {
      notes: [
        {
          id: uuidv4(), // для уникальных идентификаторов, тк в реальном приложении массив будет не статический
          title: "Заметка 1",
          todos: [
            { id: uuidv4(), text: "Задача 1" },
            { id: uuidv4(), text: "Задача 2" },
            { id: uuidv4(), text: "Задача 3" },
            { id: uuidv4(), text: "Задача 3" },
          ],
        },
        {
          id: uuidv4(),
          title: "Заметка 2",
          todos: [
            { id: uuidv4(), text: "Задача 1" },
            { id: uuidv4(), text: "Задача 2" },
            { id: uuidv4(), text: "Задача 3" },
            { id: uuidv4(), text: "Задача 3" },
          ],
        },
        {
          id: uuidv4(),
          title: "Заметка 3",
          todos: [
            { id: uuidv4(), text: "Задача 1" },
            { id: uuidv4(), text: "Задача 2" },
            { id: uuidv4(), text: "Задача 3" },
            { id: uuidv4(), text: "Задача 3" },
          ],
        },
        {
          id: uuidv4(),
          title: "Заметка 4",
          todos: [
            { id: uuidv4(), text: "Задача 1" },
            { id: uuidv4(), text: "Задача 2" },
            { id: uuidv4(), text: "Задача 3" },
            { id: uuidv4(), text: "Задача 3" },
          ],
        },
        {
          id: uuidv4(),
          title: "Заметка 5",
          todos: [
            { id: uuidv4(), text: "Задача 1" },
            { id: uuidv4(), text: "Задача 2" },
            { id: uuidv4(), text: "Задача 3" },
            { id: uuidv4(), text: "Задача 3" },
          ],
        },
        {
          id: uuidv4(),
          title: "Заметка 6",
          todos: [
            { id: uuidv4(), text: "Задача 1" },
            { id: uuidv4(), text: "Задача 2" },
            { id: uuidv4(), text: "Задача 3" },
            { id: uuidv4(), text: "Задача 3" },
          ],
        },
      ],
      modalVisible: false,
      editMode: false,
      currentNote: null,
    };
  },

  methods: {
    // универсальная функция для создания и редактирования заметок
    createEditNote(note) {
      if (this.editMode) {
        this.notes = this.notes.map((item) => {
          if (item.id === note.id) {
            return note;
          }
          return item;
        });
        this.editMode = false;
      } else {
        this.notes.push(note);
      }
      this.modalVisible = false;
      this.currentNote = null;
    },
    //функция для удаления заметок
    deleteNote(note) {
      if (confirm("Вы действительно хотите удалить заметку?")) {
        this.notes = this.notes.filter((item) => item.id !== note.id);
      }
    },
    // функция для включения режимма редактирования
    addEditMode(note) {
      this.editMode = true;
      this.currentNote = note;
      this.showModal();
      console.log(this.notes);
    },

    showModal() {
      this.modalVisible = true;
    },
  },
};
</script>

<style>
.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}

h1 {
  font-weight: bold;
  margin-bottom: 100px;
  font-size: 75px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

main {
  height: 100%;
  width: 100%;
}
</style>
