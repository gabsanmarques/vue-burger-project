<template>
  <PageNavbar />
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
};
</script>

<style></style>
