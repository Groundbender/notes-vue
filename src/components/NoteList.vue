<template>
  <ul class="notes-container">
    <note-item
      @edit="addEditMode"
      v-for="note in notes"
      :key="note.id"
      :note="note"
      @delete="$emit('delete', note)"
    />
  </ul>
</template>

<script>
import NoteItem from "./NoteItem.vue";

export default {
  components: {
    NoteItem,
  },
  props: {
    notes: {
      type: Array,
      required: true,
    },
  },
  methods: {
    addEditMode(note) {
      this.$emit("edit", note);
    },
  },
};
</script>

<style scoped>
.notes-container {
  display: flex;
  flex-wrap: wrap;
}

@media screen and (max-width: 800px) {
  .notes-container {
    justify-content: center;
  }
}
</style>
