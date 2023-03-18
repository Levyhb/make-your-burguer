<template>
  <div>
    <p>Componente de Mensagem</p>
    <div>
      <form id="burger-form">
        <div class="input-container">
          <label for="name">Nome do cliente:</label>
          <input type="text" id="name" v-model="name" placeholder="Digite o seu nome">
        </div>

        <div class="input-container">
          <label for="pao">Escolha o pão:</label>
          <select name="pao" id="pao" v-model="pao" >
            <option value="">Selecione o tipo de pão</option>
            <option v-for="pao in paes" :value="pao.tipo" :key="pao.id">
              {{ pao.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="carne">Escolha o tipo de carne:</label>
          <select name="carne" id="carne" v-model="carne">
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
            </option>
          </select>
        </div>

        <div id="opcionais-container" class="input-container">
          <label for="opcionais" id="opcionais-title">Selecione os opcionais:</label>
          <div class="checkbox-container" v-for="opcional in opcionaisData" :key="opcional.id">
            <input type="checkbox"
              name="opcionais"
              v-model="opcionais"
              :value="opcional.tipo"
              id="salame"
            >
            <span>{{ opcional.tipo }}</span>
          </div>
        </div>

        <div class="input-container">
          <input type="submit" class="submit-btn" value="Criar meu burger">
        </div>

      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'BurgerForm',
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisData: null,
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      status: 'Solicitado',
      msg: null
    }
  },
  methods: {
    async getIngredients() {
      const { data } = await axios.get("http://localhost:3000/ingredientes");
      this.paes = data.paes
      this.carnes = data.carnes
      this.opcionaisData = data.opcionais
      console.log(data);
    }
  },
  mounted() {
    this.getIngredients()
  }
}
</script>

<style scoped>
  #burger-form {
    max-width: 400px;
    margin: 0 auto 5rem;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid #FCBA03;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  #opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
  }

  #opcionais-title {
    width: 100%;
  }
  .checkbox-container {
    display: flex;
    align-self: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }

  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    font-size: 16px;
    padding: 10px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>