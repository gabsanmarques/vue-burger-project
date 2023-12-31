<template>
  <div id="burger-table">
    <MessageComponent v-if="msg !== ''" :msg="msg" />
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
          <select
            name="status"
            class="status"
            @change="updateBurguer($event, id)"
          >
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
          <button class="delete-btn" @click="deleteBurger(id)">
            Cancelar pedido
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import MessageComponent from "./MessageComponent.vue";

interface Burger {
  id: number;
  nome: string;
  carne: string;
  pao: string;
  opcionais: string[];
  status: string;
}

interface Status {
  id: number;
  tipo: string;
}

export default {
  name: "OrdersDashboard",
  data(): {
    burgers: Burger[];
    burger_id: number;
    statusData: Status[];
    msg: string;
  } {
    return {
      burgers: [],
      burger_id: 0,
      statusData: [],
      msg: "",
    };
  },
  methods: {
    async getPedidos(): Promise<void> {
      const req = await fetch("https://burger-api-odgl.onrender.com/burgers");
      const data = await req.json();
      this.burgers = data;
    },
    async getStatus(): Promise<void> {
      const req = await fetch("https://burger-api-odgl.onrender.com/status");
      const data = await req.json();
      this.statusData = data;
    },
    async deleteBurger(id: number): Promise<void> {
      const req = await fetch(
        `https://burger-api-odgl.onrender.com/burgers/${id}`,
        {
          method: "DELETE",
        }
      );
      const res = await req.json();
      console.log(res);
      this.getPedidos();
      this.msg = `Pedido ${id} cancelado com sucesso!`;
      setTimeout(() => {
        this.msg = "";
      }, 3000);
    },
    async updateBurguer(e: Event, id: number): Promise<void> {
      const target = e.target as HTMLSelectElement;
      const newStatus = target.value;
      const dataJson = JSON.stringify({ status: newStatus });
      const req = await fetch(
        `https://burger-api-odgl.onrender.com/burgers/${id}`,
        {
          method: "PATCH",
          headers: {
            "Content-Type": "application/json",
          },
          body: dataJson,
        }
      );
      const res = await req.json();
      console.log(res);

      this.msg = `Status do pedido ${id} atualizado com sucesso para "${newStatus}"`;
      setTimeout(() => {
        this.msg = "";
      }, 3000);
    },
  },
  mounted() {
    this.getPedidos();
    this.getStatus();
  },
  components: { MessageComponent },
};
</script>

<style scoped>
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
  min-height: 300px;
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
  height: 50px;
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
  height: 50px;
}

.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
