<template>
  <header>
    <h1>Notes</h1>
    <add-button @click="$emit('open')"></add-button>
  </header>
</template>

<script>
export default {
  name: "MyHeader",
  methods: {
    showModal() {
      this.$emit("showModal");
    },
  },
};
</script>

<style scoped>
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

@media screen and (max-width: 800px) {
  h1 {
    font-size: 50px;
    margin: 0 auto 50px auto;
  }
}
</style>
