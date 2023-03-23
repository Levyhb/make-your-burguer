<template>
  <div class="main-container">
    <div class="changeTable">
      <h1
        :class="{ 'selected': isOrders === true }"
        @click="manageOrders"
      >Gerenciar pedidos</h1>
      <h1
        @click="concludedOrders"
        :class="{ 'selected': isConcludedOrders === true }"
      >Pedidos Finalizados</h1>
    </div>
    <Dashboard v-if="isOrders"/>
    <CompletedOrders v-if="isConcludedOrders"/>
  </div>
</template>

<script>
import Dashboard from '@/components/Dashboard.vue';
import CompletedOrders from '@/components/CompletedOrders.vue';

  export default {
    name: "Pedidos",
    components: { Dashboard, CompletedOrders },
  data() {
    return {
      isOrders: true,
      isConcludedOrders: false,
    }
  },
  methods: {
    manageOrders() {
      this.isOrders = true;
      this.isConcludedOrders = false;
    },
    concludedOrders() {
      this.isOrders = false;
      this.isConcludedOrders = true;
    }
  }
}
</script>


<style scoped>
  .changeTable {
    display: flex;
    justify-content: space-evenly;
  }

  .changeTable h1 {
    border-bottom: 3px solid gray;
    cursor: pointer;
    padding: 10px 20px;
    border-radius: 10px 10px 0 0;
  }

  .selected {
    background-color: #FCBA03;
    color: white;
    border-left: 3px solid gray;
  }

  .notSelected {
    background-color: rgb(179, 179, 179);
  }
</style>