<template>
   <div class="main">
    <h1>Chico's Burger,</h1>
    <p >Onde o sabor é de outro mundo!!</p>
       <Message :msg="msg" v-show="msg"/>
       <div>
        <form  id="burger-form" @submit="verificar($event)">
            <div class="input-container">
                <label for="name">Nome do Cliente</label>
                <input type="text" id="name" name="name" v-model="name" placeholder="Digite seu nome">
            </div>
            <div class="input-container">
                <label for="breed">Escolha o pão:</label>
                <select name="breed" id="breed" v-model="breed">
                <option value="" selected>Selecione o seu pão</option>
                <option v-for="pao in paes" :key="pao" :value="pao['tipo']">{{pao['tipo']}}</option>
              </select>
            </div>
            <div class="input-container">
                <label for="meat">Escolha a carne:</label>
                <select name="meat" id="meat" v-model="meat" >
                <option value="" selected>Selecione a carne</option>
                <option v-for="carne in carnes" :key="carne" :value="carne['tipo']">{{ carne['tipo'] }}</option>
              </select>
            </div>
            <div id="opcionais-container" class="input-container">
                <label id="opcionais-title" for="optionals">Selecione os opcionais:</label>
                <div class="checkbox-container">

                    <div class="option" v-for="opcao in opcionaisdata" :key="opcao">
                      <input type="checkbox" :id="'option'+opcao['id']" v-model="optionals" :value="opcao['tipo']">
                    <span>{{opcao['tipo']}}</span>
                    </div>
                   
                </div>
            </div>
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Criar meu Hamburguer!">
            </div>
        </form>
       </div>
   </div>
</template>

<script>
import Message from './Message.vue'

export default {
    name: 'BurgerForm',
    data(){
        return{
          paes: null,
          carnes: null,
          opcionaisdata: null,
          name: null,
          breed: null,
          meat: null,
          optionals: [],
          status: 'Solicitado',
          msg: null

        }
    },
    methods: {
      verificar(e) {
        e.preventDefault();
    if (!this.name|| !this.breed || !this.meat) {
      
      this.msg = 'Preencha todos os campos!';

      setTimeout(() => this.msg = "", 3000);//limpar msg
    } else {  
        this.createBurger(e);
    }
  },

        async getIngredientes(){
          const req = await fetch("http://localhost:3000/ingredientes");
          const data = await req.json();

          console.log(data);
          this.paes = data.paes;
          this.carnes = data.carnes;
          this.opcionaisdata = data.opcionais;
          },

        async createBurger(e){
          e.preventDefault();

          const data = {
            nome: this.name,
            pao: this.breed,
            carne: this.meat,
            opcionais: Array.from(this.optionals),
            status: "Solicitado"
          }

          const dataJson = JSON.stringify(data);

          const req = await fetch("http://localhost:3000/burgers", {
            method: "POST",
            headers: {"Content-Type": "application/json"},
            body: dataJson
          });

          const resp = await req.json();

          this.msg = `Pedido N°${resp.id} realizado com sucesso!`;

          
          setTimeout(() => this.msg = "", 3000);//limpar msg

          this.name = '';
          this.breed = '';
          this.meat = '';
          this.optionals = [];
        }
    },
    mounted(){
        this.getIngredientes();
    },
    components: {
      Message
    }
}
</script>
<style scoped>
p{
  background-color: #fcba03;
  padding: 0 1rem !important;
  margin-bottom: 1rem  !important;
}

.option{
  color: #222;
}

.main{
  background-image: url(../../public/img/astro.png);
  background-size: contain;
  background-repeat: no-repeat;
  background-position: 100% 0;
  
  width: 100% !important;
  height: 100vh !important;
  display: flex !important;
  justify-content: center !important;
  align-items: center !important;
  flex-direction: column !important;
}
  #burger-form {
    background-color: #ffffff80;
    box-shadow: 0px 10px 15px rgba(0, 0, 0, 0.3);
    padding: 1rem !important;
    width: 100%;
    margin: 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
     transition: 0 !important;
  }
  #burger-form:hover{
    background-color: #ffffffe1;
    box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.384);
    border-radius: 1rem;
    transition: 0 !important;
  }

  .input-container {
    display: flex;
    justify-content: center;
    flex-direction: column;
    margin-bottom: 20px !important;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px !important;
    color: #222;;
    padding: 5px 10px !important;
    border-left: 4px solid #fcba03;
  }

  input, select {
    padding: 5px 10px !important;
    width: 300px;
  }

    #opcionais-container {
      width: 300px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: stretch;
  }

  #opcionais-title {
    width: 100%;
  }

  .checkbox-container {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    width: 100%; 
    min-height: 50px;
    margin-bottom: 20px;
  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto !important;
  }

  .checkbox-container span, .option {
    margin-left: 6px !important;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
    border-radius: 1rem;
  }
</style>