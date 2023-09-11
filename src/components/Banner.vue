<template>
    <div id="main-banner">
        <h1>Make Your Burguer</h1>
    </div>
</template>

<script>
export default {
    name: 'Banner'
}
</script>

<style scoped>
#main-banner {
    background-image: url('/img/burger.jpg');
    background-position: 0 -60vh;
    background-size: fit;
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
    border-radius: 0.5rem;
}
</style>