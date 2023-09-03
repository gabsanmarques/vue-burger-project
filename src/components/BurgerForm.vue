<template>
  <div>
    <p>Message Component</p>
    <div>
      <form id="burger-form">
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
            <option value="whole-grain">Integral</option>
          </select>
        </div>

        <div class="input-container">
          <label for="patty"> Escolha a carne: </label>
          <select name="patty" id="patty-select" v-model="patty">
            <option value="">Selecione o tipo de carne...</option>
            <option value="rump-skirt">Maminha</option>
          </select>
        </div>

        <div class="input-container" id="optional-container">
          <label id="optional-title" for="optional">
            Escolha os opcionais:
          </label>
          <div class="checkbox-container">
            <input
              type="checkbox"
              name="optional"
              v-model="optional"
              value="salami"
            /><span>Salame</span>
          </div>
          <div class="checkbox-container">
            <input
              type="checkbox"
              name="optional"
              v-model="optional"
              value="salami"
            /><span>Salame</span>
          </div>
          <div class="checkbox-container">
            <input
              type="checkbox"
              name="optional"
              v-model="optional"
              value="salami"
            /><span>Salame</span>
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
export default {
  name: "BurgerForm",
  data() {
    return {
      name: "",
      bread: "",
      patty: "",
      optional: [],
    };
  },
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
