<template>
  <footer>
    <ul>
      <li v-for="(item, index) in submenu" :key="index">
        {{ item }}
      </li>
      <!--
      <li>Productos</li>
      <li v-if="!isMobile">Servicios</li>
      <li v-else>Servicios Mobile</li>
      <li>Contacta</li>
      -->
    </ul>
  </footer>
</template>

<script>
export default {
  // props: ["isMobile", "submenu"],
  props: {
    isMobile: {
      required: true,
      type: Boolean,
      default: true,
    },
    submenu: {
      required: false,
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
ul {
  display: flex;
  gap: 4em;
}
li {
  list-style-type: none;
}
</style>