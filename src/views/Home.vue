<template>
  <Banner />
  <div class="main-container">
    <h1>Monte o seu Burger</h1>
    <p></p>
  </div>
</template>

<script>
import Banner from '@/components/Banner.vue';
import Navbar from '@/components/Navbar.vue';

  export default {
    components: { Navbar, Banner }
}
</script>