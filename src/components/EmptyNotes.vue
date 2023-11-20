<template>
  <div class="empty-wrapper">
    <h1 class="empty-message">Заметок пока нет</h1>
  </div>
</template>

<script>
export default {
  name: "EmptyNotes",
};
</script>

<style scoped>
.empty-wrapper {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.empty-message {
  font-size: 50px;
  font-weight: bold;
}
</style>
