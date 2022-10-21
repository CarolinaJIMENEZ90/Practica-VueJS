<template>
    <div id="burger-table">
       <div>
        <div id="cabeza-tabla">
            <div class="orde-id">#:</div>
            <div>Cliente:</div>
            <div>Pam</div>
            <div>Carnes</div>
            <div>Opcionais</div>
            <div>Acciones</div>
        </div>
       </div>
       <div id="burger-table-rows">
        <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
            <div class="orden-number">{{burger.id}}</div>
            <div>{{burger.nome}}</div>
            <div>{{burger.pao}}</div>
            <div>{{burger.carne}}</div>
            <div>
                <ul>
                    <li v-for="(opcional,index) in burger.opcionais" :key="index">{{opcional}}</li>
                  
                </ul>
            </div>
            <div>
                <select name="status" class="status" @change="updateBurge($event, burger.id)">
                    <option value="">Selecione</option>
                    <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo" >
                      {{s.tipo}}
                      </option>
                </select>
                <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
            </div>
        </div>
       </div>
    </div>
</template>

<script>
export default{
    name:"Tabla",
    data(){
      return{
        burgers:null,
        burgers_id:null,
        status:[]
      }
    },
    methods:{
 async getPedidos(){
const req= await fetch("http://localhost:3000/burgers");
const data= await req.json();
this.burgers=data;
console.log(this.burgers);

//resgatar status

this.getStatus();
 },
 async getStatus(){
const req= await fetch("http://localhost:3000/status");
const data= await req.json();
this.status=data;

 },
  async deleteBurger(id){
const req= await fetch(`http://localhost:3000/burgers/${id}`,{
method:"DELETE"
});
const res= await req.json();

this.getPedidos();

    },
    async updateBurger(event, id){
     const opcion=event.target.value;
     const dataJson= JSON.stringify({status:opcion});
     const req= await fetch(`http://localhost:3000/burgers/${id}`,{
    method:"PATCH",
    headers:{"Content-Type": "application/json"},
    body:dataJson
});
const res= await req.json();
console.log(res)

    }
    },
    mounted(){
      this.getPedidos();
    }
}
</script>
 <style scoped>
 #burger-table{
    max-width: 12000px;
    margin: 0 auto;
 }
 #cabeza-tabla,
 #burger-table-rows,
 .burger-table-row{
    display: flex;
    flex-wrap: wrap;
 }
  #cabeza-tabla{
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
 }
  #cabeza-tabla div,
  .burger-table-row div{
    width: 19%;
  }
  .burger-table-row{
    width: 100%;
    padding: 12px;
    border: 1px solid green;
  }
  #cabeza-tabla .orde-id,
   .burger-table-row .orden-number{
     width: 5%;

  }

  select{
    padding: 12px 6px;
    margin-right: 12px;
  }
  .delete-btn{
    background-color: #08f070;
    color:rgb(218, 8, 8);
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    margin: 0% auto;
    cursor: pointer;
    transition: 5s;
  }

  .delete-btn:hover{
    background-color: transparent;
    color: black;
  }
 </style>