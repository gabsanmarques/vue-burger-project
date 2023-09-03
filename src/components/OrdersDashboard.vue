<template>
  <div id="burger-table">
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações</div>
      </div>
    </div>
    <div id="burger-table-rows">
      <div
        v-for="{ id, nome, carne, pao, opcionais, status } in burgers"
        class="burger-table-row"
        :key="id"
      >
        <div class="order-number">{{ id }}</div>
        <div>{{ nome }}</div>
        <div>{{ pao }}</div>
        <div>{{ carne }}</div>
        <div>
          <ul>
            <li v-for="(item, index) in opcionais" :key="index">{{ item }}</li>
          </ul>
        </div>
        <div>
          <select name="status" class="status">
            <option value="">Selecione o status do pedido...</option>
            <option
              v-for="{ id, tipo } in statusData"
              :value="tipo"
              :key="id"
              :selected="status === tipo"
            >
              {{ tipo }}
            </option>
          </select>
          <button class="delete-btn">Cancelar pedido</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: "OrdersDashboard",
  data() {
    return {
      burgers: [],
      burger_id: 0,
      statusData: [],
    };
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");
      const data = await req.json();

      this.burgers = data;
    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      const data = await req.json();

      this.statusData = data;
    },
  },
  mounted() {
    this.getPedidos();
    this.getStatus();
  },
};
</script>

<style scoped>
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}

#burger-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px solid #333;
}

#burger-table-heading div,
.burger-table-row div {
  width: 19%;
  display: flex;
}

.burger-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #333;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
}

select {
  padding: 12px 6px;
  margin-right: 12px;
  width: 50%;
}

.delete-btn {
  background-color: #222;
  padding: 5px;
  color: #fcba0f;
  font-weight: bold;
  border: 2px solid #222;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
