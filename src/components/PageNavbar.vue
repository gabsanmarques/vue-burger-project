<template>
  <nav>
    <router-link to="/">
      <img src="" alt="Burger Shop Logo" />
    </router-link>
    <router-link to="/">Home</router-link>
    <router-link to="/orders">Orders</router-link>
  </nav>
</template>

<script lang="ts">
export default {
  name: "PageNavbar",
};
</script>

<style scoped>
nav {
  display: flex;
  gap: 20px;
}
</style>
