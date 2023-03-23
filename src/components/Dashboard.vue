<template>
  <div id="burger-table">
    <Message :msg="msg" v-show="msg" :statusMsg="statusMsg"/>
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#</div>
        <div class="">Cliente:</div>
        <div class="">Pão:</div>
        <div class="">Carne:</div>
        <div class="">Opcionais:</div>
        <div class="">Ações:</div>
      </div>
      <div id="burger-table-rows" v-for="burger in burgers" :key="burger.id"  v-show="burger.status !== 'Finalizado'">
        <div class="burger-table-row">
          <div class="order-number">{{ burger.id }}</div>
          <div>{{ burger.nome }}</div>
          <div>{{ burger.pao }}</div>
          <div>{{ burger.carne}}</div>
          <div>
            <ul>
              <li v-for="(opcional, index) in burger.opcionais" :key="index">
                {{ opcional }}
              </li>
            </ul>
          </div>
          <div>
            <select name="status" class="status" @change="updateStatus($event, burger.id)">
              <option value="">Selecione</option>
              <option
                v-for="s in status"
                :key="s.id"
                :value="s.tipo"
                :selected="burger.status === s.tipo"               
              >
                {{ s.tipo }}
              </option>
            </select>
            <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
          </div>
        </div>
        
      </div>

    </div>
  </div>
</template>

<script>
  import axios from 'axios';
  import Message from "./Message.vue";

  export default {
  name: "Dashboard",
  data () {
    return {
      burgers: null,
      status: [],
      msg: null,
      statusMsg: null
    }
  },
  methods: {
    async getStatus() {
      const { data } = await axios.get('http://localhost:3000/status');
      this.status = data;
    },
    async getOrders() {
      const req = await axios.get('http://localhost:3000/burgers');
      this.burgers = req.data;
      this.getStatus();
    },
    async deleteBurger(id) {
      await axios.delete(`http://localhost:3000/burgers/${id}`);
      this.getOrders();
      this.msg = `Pedido Nº ${id} removido sucesso`
      setTimeout(() => this.msg = "", 3000)
      this.statusMsg = 204;
    },
    async updateStatus(event, id) {
      const option = event.target.value;
      const dataJson = { status: option }
      const req = await axios.patch(`http://localhost:3000/burgers/${id}`, dataJson)
      this.msg = `Status do pedido Nº ${id} atualizado para "${req.data.status}"`
      setTimeout(() => this.msg = "", 3000)
      this.getOrders();
      this.statusMsg = 200;
    }
  },
  mounted() {
    this.getOrders();
  },
  components: {
    Message
  }
  }
</script>

<style>
  #burger-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #burger-table-heading,
  #burger-table-rows,
  .burger-table-row {
    display: flex;
    align-items: center;
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
  }

  .burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  #burger-table-heading .order-id, .burger-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
  }

  .delete-btn {
    background-color: #222;
    color: #FCBA03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }

</style>