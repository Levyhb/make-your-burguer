<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: 'Message',
  props: {
    msg: String
  }
}
</script>

<style>
  .message-container {
    color:  #006305;
    background-color: #d2ffcc;
    border: 2px solid #c9ffb8;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
    animation: fadeIn .7s;
  }

  @keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}

</style>