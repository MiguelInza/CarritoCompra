<template>
  <header>
    <img src="../assets/logo.png" width="32" />
    <div>My carrito superpower</div>
    <div>{{ count }}</div>
    <button @click="showCount">Show count!</button>
  </header>
</template>

<script>
export default {
  props: ["count"],
  methods: {
    showCount() {
      alert(this.count);
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
}
</style>