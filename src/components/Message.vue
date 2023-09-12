<template>
  <div class="message-container">
    <p>{{ msg }}</p>
  </div>
</template>

<script>
  export default {
    name: "Message",
    props: {
      msg: String
    }
  }
</script>

<style scoped>
  .message-container {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #004085;
    background-color: #cce5ff;
    border: 2px solid #b8daff;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px 0.5rem !important;

  }
  .message-container p{
    font-size: calc(0.5rem + 0.75vw);
  }
</style>