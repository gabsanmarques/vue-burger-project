<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script lang="ts">
export default {
  name: "MessageComponent",
  props: {
    msg: {
      type: String,
      required: true,
    },
  },
};
</script>

<style scoped>
.message-container {
  color: #004085;
  background-color: #cce5ff;
  border: 2px solid #b7daff;
  border-radius: 5px;
  padding: 10px;
  max-width: 400px;
  margin: 30px auto;
}
</style>
