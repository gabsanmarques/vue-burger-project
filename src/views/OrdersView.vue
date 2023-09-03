<template>
  <div class="main-container">
    <h1>Gerenciar pedidos</h1>
    <OrdersDashboard />
  </div>
</template>

<script lang="ts">
import OrdersDashboard from "@/components/OrdersDashboard.vue";

export default {
  name: "OrdersView",
  components: { OrdersDashboard },
};
</script>

<style scoped></style>
