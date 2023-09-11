<template>
  <div id='box-nav'>
    <div id="nav">
      <router-link id="logo-url" to="/">
        <img id="logo" :src="logo" :alt="alt">
      </router-link>
      <div class="botoes">
      <router-link to="/">Fazer Pedido</router-link>
      <router-link to="/pedidos">Pedidos</router-link>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "Navbar",
  props: ["logo", "alt"]
}
</script>

<style scoped>
  #box-nav{
    box-shadow: #000000 10px 10px 10px 10px !important;
  }

  #nav {
    background-color: #222;
    border-bottom: 4px solid #111111a9;
    box-shadow: 10px 10px 10px 10px #000000;
    padding: 15px 50px !important;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

  #nav #logo-url {
    margin: auto !important;
    margin-left: 0 !important;
  }

  #logo {
    width: 40px;
    height: 40px;
  }

  #nav a {
    color: #fcba03;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
  }

  #nav a:hover {
    color: #FFF;
  }
  .botoes {
    display: flex;
    justify-content: space-around;
    align-items: center;
    min-width: 30vw;
    max-width: 100px !important;
  }
</style>