<template>
  <footer id="footer">
    <p>Make Your Burger &copy; 2023</p>
  </footer>
</template>

<script>
  export default {
    name: "Footer"
  }
</script>

<style scoped>
  #footer{
    height: 7vh;
    background-color: #222;
    border-top: 4px solid #111;
    position: fixed;
    color: #FCBA03;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    bottom: 0%;
  }
</style>