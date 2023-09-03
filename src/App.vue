<template>
  <PageNavbar :logo="logo_src" :alt="app_name" />
  <router-view />
  <PageFooter />
</template>

<script lang="ts">
import PageFooter from "./components/PageFooter.vue";
import PageNavbar from "./components/PageNavbar.vue";

export default {
  components: {
    PageNavbar,
    PageFooter,
  },
  data() {
    return {
      logo_src: "/img/logo.png",
      app_name: "Make Your Burger",
    };
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Helvetica, sans-serif;
}

html,
body {
  height: 100%;
}

.main-container {
  margin: 50px;
  min-height: 250px;
}

h1 {
  text-align: center;
  font-size: 42px;
  margin-bottom: 30px;
  color: #222;
}
</style>
