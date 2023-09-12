<template>
<div class="main">
    <Message :msg="msg" v-show="msg"/>
  <table id="burger-table" v-if="burgers">
    
  <thead>
    <tr id="burger-table-heading">
      <th class="order-id">#:</th>
      <th>Cliente:</th>
      <th>Pão:</th>
      <th>Carne:</th>
      <th>Opcionais:</th>
      <th>Ações:</th>
    </tr>
  </thead>
  <tbody id="burger-table-rows">
    <tr class="burger-table-row" v-for="burger in burgers" :key="burger.id">
      <td class="order-number">{{ burger.id }}</td>
      <td>{{ burger.nome }}</td>
      <td>{{ burger.pao }}</td>
      <td>{{ burger.carne }}</td>
      <td>
        <ul>
          <li class="li" v-for="(opcional, index) in burger.opcionais" :key="index">-> {{ opcional }}</li>
        </ul>
      </td>
      <td>
         <select name="status"  @change="updateBurger($event, burger.id)">
            <option :value="s.tipo" v-for="s in status" :key="s.id" :selected="burger.status == s.tipo">
            {{ s.tipo }}
            </option>
          </select>
        <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
      </td>
    </tr>
  </tbody>
</table>

<div v-else>
  <h2>Não há pedidos no momento!</h2>
</div>
</div>
</template>
<script>
import Message from '@/components/Message.vue';

export default {
    name: 'Dashboard',
    data(){
        return {
             burgers: null,
            burger_id: null,
            status: [],
            msg: null
        }
    },
    methods: {
        async getPedidos(){
            const req = await fetch('http://localhost:3000/burgers');
            const data = await req.json();
            this.burgers = data;

            this.getStatus()

        },
         async getStatus() {

        const req = await fetch('http://localhost:3000/status')

        const data = await req.json()

        this.status = data

      },

        async deleteBurger(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'DELETE'
            });

            const res = await req.json();

            this.msg = 'Pedido removido com sucesso!'
             setTimeout(() => this.msg = "", 3000);//limpar msg
            this.getPedidos();

        },
       async updateBurger(event, id) {
        try {
            // Prepare os dados que deseja atualizar, por exemplo, o novo status.
            const novoStatus = event.target.value;

            const requestBody = {
            status: novoStatus,
            };

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
            method: 'PATCH',
            headers: {
                'Content-Type': 'application/json', 
            },
            body: JSON.stringify(requestBody), // Converte o corpo em JSON.
            });

            if (req.ok) {
            this.msg = `O pedido N° ${id} foi atualizado com sucesso!`

            this.getPedidos();
            } else {
            // Trate erros de requisição, por exemplo, exibindo uma mensagem de erro.
            this.msg = 'Erro ao atualizar o pedido do hambúrguer';
            }
             setTimeout(() => this.msg = "", 3000);//limpar msg
        } catch (error) {
            console.error('Ocorreu um erro durante a atualização:', error);
        }
        }

    },
    mounted(){
        this.getPedidos();
    },
    components:{
        Message
    }
}
</script>
<style scoped>
.main{
    max-width: 90vw;
    min-height: 50vh;
    margin: 0 auto !important;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding-bottom: 2rem !important;
}
  #burger-table {
    width: 100%;
    margin: 0 auto;
    border: none;
    border-bottom: 2rem !important;
  }
  #burger-table-heading {
    margin: 1rem 2rem !important;
  }

  table {
    width: 100%;
    border: 1px solid #333;
  
  }
  table thead{
    width: 100% !important;
  }
  tbody tr{
    margin: 1rem !important;
  }
  tbody tr:hover{
     box-shadow: 0 7px 7px 0px rgba(0, 0, 0, 0.466);
  }

  th, td {
    text-align: left;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  th {
    text-align: center;
    background-color: #333;
    color: white;
    height: 48px ;
    
  }
  th:nth-child(1){
      border-radius: 48px !important;
      color: #fcba03;
  }
  td:nth-child(1){
     text-align: center;
     width: 48px;
     height: 48px;
  }

  td {
    vertical-align: middle;
    text-align: center;
    min-height: 1rem;
    padding: 1rem 0.5rem !important;
  }
  td:nth-child(1){
      border-radius: 0.5rem 0rem 0 0.5rem !important;
  }
   td:nth-last-child(1){
      border-radius: 0rem 0.5rem 0.5rem 0rem !important;
  }
  .li{
    list-style: none;
    text-overflow: ellipsis; 
  }

  select {
    padding: 10px !important;
    margin-right: 12px !important;
  }

  .delete-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px !important;
    font-size: 16px ;
    cursor: pointer;
    transition: background-color 0.5s, color 0.5s;
  }

  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }

</style>
