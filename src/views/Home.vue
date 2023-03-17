<template>
  <Banner />
  <div class="main-container">
    <h1>Monte o seu Burger</h1>
    <BurgerForm />
  </div>
</template>

<script>
import Banner from '@/components/Banner.vue';
import BurgerForm from '@/components/BurgerForm.vue';
import Navbar from '@/components/Navbar.vue';

  export default {
    components: { Navbar, Banner, BurgerForm }
}
</script>

<style scoped>
  
</style>