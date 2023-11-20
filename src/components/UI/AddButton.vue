<template>
  <button class="add-btn" @click="showModal">+</button>
</template>

<script>
export default {
  name: "AddButton",
  methods: {
    showModal() {
      this.$emit("showModal");
    },
  },
};
</script>

<style scoped>
.add-btn {
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  border-radius: 1000px;
  color: white;
  font-size: 20px;
  font-weight: bold;
  transition: transform 0.2s ease-in-out;
}

.add-btn:hover {
  transform: scale(1.1);
  background-color: blueviolet;
}

.add-btn:active {
  transform: scale(0.9);
  background-color: gray;
}
</style>
