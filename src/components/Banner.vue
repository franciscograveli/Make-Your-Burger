<template>
    <div id="main-banner">
        <h1>Make Your Burger</h1>
    </div>
</template>

<script>
export default {
    name: 'Banner',
    data(){
        return{
            link1: ["url('/img/burger.jpg')","url('/img/burger2.png')","url('/img/burger3.jpg')"]
        }
    },
    mounted() {
  // Verifique se o elemento com ID "main-banner" existe no DOM.
  const mainBanner = document.getElementById('main-banner');
  if (mainBanner) {
    const linksDeFundo = Array.from(this.link1);
    let index = 0;

    function trocarBanner() {
      mainBanner.style.backgroundImage = linksDeFundo[index];
      index = (index + 1) % linksDeFundo.length;

      // Agende a próxima troca de banner após 10 segundos.
      setTimeout(trocarBanner, 15000);
    }

    // Inicie a troca de banner.
    trocarBanner();
  }
}

}
</script>

<style scoped>
#main-banner {
    background-image: url('/img/burger.jpg')  ;
    background-position: center;
    background-size: cover;
    height: 90vh;
    display: flex !important;
    align-items: center !important;
    justify-content: start !important;
}

#main-banner h1{
    color: #fff;
    text-align: center;
    font-size: 50px;
    background-color: #222;
    padding: 20px 40px !important;
    
}
</style>