<template>
  <div id="burger-table">
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#</div>
        <div class="">Cliente:</div>
        <div class="">Pão:</div>
        <div class="">Carne:</div>
        <div class="">Opcionais:</div>
        <div class="">Status:</div>
      </div>
      <div id="burger-table-rows" v-for="burger in burgers" :key="burger.id">
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
            <span class="concluded-order">Finalizado</span>
          </div>
        </div>
        
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'CompletedOrders',
  data() {
    return {
      burgers: null,
    }
  },
  methods: {
    async getFinishedOrders() {
      const { data } = await axios.get('http://localhost:3000/burgers');
      const burgersFinished = data.filter((e) => e.status === "Finalizado");
      console.log(burgersFinished);
      this.burgers = burgersFinished;
    }
  },
  mounted() {
    this.getFinishedOrders();
  },
}
</script>

<style>
  .concluded-order {
    padding: 7px;
    border-radius: 5px;
    font-size: 18px;
    background-color: rgb(151, 255, 151);
    color: rgb(0, 70, 0);
  }
</style>