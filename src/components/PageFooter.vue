<template>
  <footer id="footer">
    <p>Make Your Burger &copy; 2023</p>
    <p>Made by Gabriel Santos</p>
  </footer>
</template>

<script lang="ts">
export default {
  name: "PageFooter",
};
</script>

<style scoped>
footer {
  height: 200px;
  background-color: #222;
  color: #fcba03;
  bottom: 0;
  display: flex;
  flex-direction: column;
  text-align: center;
  justify-content: center;
  width: 100%;
}
</style>
