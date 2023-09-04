<template>
  <div>
    <MessageComponent v-if="!(msg === '')" :msg="msg" />
    <div>
      <form ref="burgerForm" id="burger-form" @submit="createBurger($event)">
        <div class="input-container">
          <label for="name"> Nome: </label>
          <input
            type="text"
            name="name"
            id="name-input"
            v-model="name"
            placeholder="Digite seu nome.."
          />
        </div>

        <div class="input-container">
          <label for="bread"> Escolha o pão: </label>
          <select name="bread" id="bread-select" v-model="bread">
            <option value="">Selecione o tipo de pão...</option>
            <option v-for="{ id, tipo } in breads" :value="tipo" :key="id">
              {{ tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="patty"> Escolha a carne: </label>
          <select name="patty" id="patty-select" v-model="patty">
            <option value="">Selecione o tipo de carne...</option>
            <option v-for="{ id, tipo } in patties" :value="tipo" :key="id">
              {{ tipo }}
            </option>
          </select>
        </div>

        <div class="input-container" id="optional-container">
          <label id="optional-title" for="optional">
            Escolha os opcionais:
          </label>
          <div
            v-for="{ id, tipo } in optionalData"
            class="checkbox-container"
            :key="id"
          >
            <input
              type="checkbox"
              name="optional"
              v-model="optional"
              :value="tipo"
            /><span>{{ tipo }}</span>
          </div>
        </div>

        <div class="input-container">
          <input type="submit" class="submit-btn" value="Fazer Pedido" />
        </div>
      </form>
    </div>
  </div>
</template>

<script lang="ts">
import MessageComponent from "./MessageComponent.vue";

export default {
  name: "BurgerForm",
  data() {
    return {
      breads: [],
      patties: [],
      optionalData: [],
      name: "",
      bread: "",
      patty: "",
      optional: [],
      msg: "",
    };
  },
  methods: {
    async getIngredients() {
      const req = await fetch(
        "https://burger-api-odgl.onrender.com/ingredientes"
      );
      const data = await req.json();
      this.breads = data.paes;
      this.patties = data.carnes;
      this.optionalData = data.opcionais;
    },
    async createBurger(e: Event) {
      e.preventDefault();

      const data = {
        nome: this.name,
        carne: this.patty,
        pao: this.bread,
        opcionais: Array.from(this.optional),
        status: "Solicitado",
      };
      const dataJson = JSON.stringify(data);
      const req = await fetch("https://burger-api-odgl.onrender.com/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

      const res = await req.json();
      this.msg = `Pedido Nº ${res.id} feito com sucesso!`;
      setTimeout(() => (this.msg = ""), 3000);

      this.name = "";
      this.patty = "";
      this.bread = "";
      this.optional = [];
    },
  },
  mounted() {
    this.getIngredients();
  },
  components: { MessageComponent },
};
</script>

<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 10px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}

input,
select {
  padding: 5px 10px;
  width: 300px;
}

#optional-container {
  flex-direction: row;
  flex-wrap: wrap;
}

#optional-title {
  width: 100%;
}

.checkbox-container {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
  width: auto;
}

.checkbox-container span {
  font-weight: bold;
  margin-left: 6px;
}

.submit-btn {
  background-color: #222;
  color: #fcab03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 10px;
  font-size: 16px;
  /*margin: 0 auto;*/
  cursor: pointer;
  transition: 0.2s;
}

.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
