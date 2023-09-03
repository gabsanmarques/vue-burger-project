<template>
  <div id="main-banner">
    <h1>Make Your Burger</h1>
  </div>
</template>

<script lang="ts">
export default {
  name: "MainBanner",
};
</script>

<style scoped>
#main-banner {
  background-image: url("/public/img/burger.jpg");
  background-position: 0 70%;
  background-size: cover;
  background-repeat: no-repeat;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

#main-banner h1 {
  color: #fff;
  text-align: center;
  font-size: 60px;
  padding: 20px 40px;
}
</style>
