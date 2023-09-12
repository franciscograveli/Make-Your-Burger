<script>
import { RouterLink, RouterView } from 'vue-router';
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';

export default {
  components: {
        Navbar,
        Footer
    },
  data(){
    return {
      logo_src: '/img/logo.png',
      app_name: 'Make Your Burguer'
    }
  }
}
</script>

<template>
<Navbar :logo="logo_src" :alt="app_name"/>
<RouterView />
<Footer />
</template>

<style>
*{
  transition: .5s;
  margin: 0!important;
  padding: 0!important;
  box-sizing: border-box; 
  font-family: Arial, Helvetica, sans-serif;
  
}
body{
   background-color: #ddd;
   color: #222;
}
#app{
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: space-between;
  min-height: 100vh;
  min-width: 100vw;
}

.main-container{
  margin: 50px;
  min-height: 50vh;
}

h1{
  text-align: center;
  font-size: 2rem;
  margin-bottom: 2rem;
  color: #222;
  font-weight: bold;
}
</style>
