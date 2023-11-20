<template>
  <div class="modal" v-if="show" @click="closeModal">
    <div @click.stop="" class="modal-content">
      <h2 class="modal-title">{{ editMode ? "Edit note" : "Create note" }}</h2>
      <slot></slot>
    </div>
  </div>
</template>

<script>
// модалка закрывается по клику на overlay
export default {
  name: "Modal",

  props: {
    show: {
      type: Boolean,
      default: false,
    },

    editMode: {
      type: Boolean,
      default: false,
    },

    currentNote: {
      type: Object,
      default: null,
    },
  },

  methods: {
    // при закрытии модалки (если мы не редактирвоали и ничего не создавали) в любом случае очищаем данные ниже поля
    closeModal() {
      this.$emit("update:show", false);
      this.$emit("update:editMode", false);
      this.$emit("update:currentNote", null);
    },
  },
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2;
}

.modal-content {
  margin: auto;
  background: #282828;
  border-radius: 12px;
  min-height: 100px;
  min-width: 300px;
  padding: 40px;
  animation: open 0.2s ease-in-out forwards;
}

.modal-title {
  font-weight: bold;
  margin-bottom: 25px;
}

@keyframes open {
  from {
    transform: scale(0);
  }
  to {
    transform: scale(1);
  }
}
</style>
