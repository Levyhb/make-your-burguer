<template>
  <div
    :class="{
        'message-container atualizado': statusMsg === 200,
        'message-container criado': statusMsg === 201,
        'message-container deletado': statusMsg === 204
      }"
  >
    <p>{{ msg }}</p>
  </div>
</template>

<script>
export default {
  name: 'Message',
  props: {
    msg: String,
    statusMsg: Number
  }
}
</script>

<style>
  .message-container {
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
    animation: fadeIn .7s;
    text-align: center;
  }

  .criado {
    color:  #006305;
    background-color: #d2ffcc;
    border: 2px solid #c9ffb8;
  }

  .atualizado {
    color:  #002363;
    background-color: #81acfd;
    border: 2px solid #5e96fd;
  }

  .deletado {
    color:  #4d0101;
    background-color: #ff6e6e;
    border: 2px solid #ff5656;
  }

  @keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}

</style>