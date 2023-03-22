<template>
  <div>
    <Message :msg="msg" v-show="msg" :statusMsg="statusMsg"/>
    <div>
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="name">Nome do cliente:</label>
          <input
            type="text"
            id="name"
            v-model="nome"
            placeholder="Digite o seu nome"
            required
          >
        </div>

        <div class="input-container">
          <label for="pao">Escolha o pão:</label>
          <select name="pao" id="pao" v-model="pao" required>
            <option value="">Selecione o tipo de pão</option>
            <option v-for="pao in paes" :value="pao.tipo" :key="pao.id">
              {{ pao.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label for="carne">Escolha o tipo de carne:</label>
          <select name="carne" id="carne" v-model="carne" required>
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
import Message from "./Message.vue";
export default {
    name: "BurgerForm",
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisData: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            status: "Solicitado",
            msg: null,
            statusMsg: null
        };
    },
    methods: {
        async getIngredients() {
            const { data } = await axios.get("http://localhost:3000/ingredientes");
            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisData = data.opcionais;
        },
        async createBurger(e) {
            e.preventDefault();
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            };

            const dataJson = JSON.stringify(data);
            const req = await fetch("http://localhost:3000/burgers", {
              method: "POST",
              headers: { "Content-Type": "application/json" },
              body: dataJson
            });
            const res = await req.json();

            this.msg = `Pedido Nº ${res.id} Realizado Com sucesso`
            setTimeout(() => this.msg = "", 3000)
            this.statusMsg = 201;

            this.nome = "";
            this.carne = "";
            this.opcionais = [];
            this.pao = "";
        }
    },
    mounted() {
        this.getIngredients();
    },
    components: { Message }
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