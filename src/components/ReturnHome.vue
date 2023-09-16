<template>
<div>
    <div class="d-flex-center">
        <button type="button" @click="returnHome()">Fazer Pedido</button>
    </div>
</div>
</template>

<script>
export default {
    name: 'ReturnHome',
    methods:{
        returnHome(){
            this.$router.push('/');
        }
    }
}
</script>
<style scoped>
.d-flex-center{
    width: 100%;
    display: flex !important;
    justify-content: center !important;
    align-items: center !important;
    flex-direction: column !important;
    align-content: center !important;
}

button{
    color: #fcba03 !important;
    text-decoration: none;
}

button{
    background-color: #222;
    border: 3px solid #222;
    padding: 1rem 2rem !important;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 auto;
    margin-top: 2rem;
    margin-bottom: 2rem;
    transition: 0.5s;
    font-weight: bolder;
}

button:hover{
    border-radius: 2rem;
    cursor: pointer;
    background-color: transparent;
    color: #222 !important;
}

</style>