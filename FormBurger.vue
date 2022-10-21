<template>
    <div id="burger">
       <Mensaje :msg="msg" v-show="msg"/>
    <div>
     <form  id="burger-form" @submit="createBurger" >
     <div class="input-container">
      <label for="nome">Nombre del Cliente:</label>
      <input type="text" id="nome" name="nome" v-model="nome" placeholder="Escriba su Nombre">
     </div>
      <div class="input-container">
      <label for="pao">Escoja el Pam:</label>
      <select name="pao" id="pao" v-model="pao">
      <option value="">Seleccione su pan</option>
      <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{pao.tipo}}</option>
      </select>
     </div>
     <div class="input-container">
      <label for="carne">Escoja la Carne:</label>
      <select name="carne" id="carne" v-model="carne">
      <option value="">Seleccione el tipo  Carne</option>
     <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
      </select>
     </div>
     <div  id="opcion-container" class="input-container">
      <label id="opcione-labe" for="opcionais">Seleciones su opcion:</label>
     <div class="opcion-container" v-for="opcional in opcionaisdata" :key="opcional.id">
     <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
     <span> {{opcional.tipo}}</span>
     
     </div>
      </div>
    <div class="input-container">
        <input type="submit" class="submit-btn" value="Pide Tu Burger">

    </div>
     </form>
    </div>
 </div>
  
</template>
<script>
import Mensaje from './Mensaje.vue'
export default{
    name:"FormBurger",

    components:{
        Mensaje
    },
    data(){
        return{
            paes:null,
            carnes:null,
            opcionaisdata:null,
            nome:null,
            pao :null,
            carne:null,
            opcionais:[],
            msg:null
        }
    },
    methods:{
      async getIngredientes() {
        const req= await fetch("http://localhost:3000/ingredientes");
        const data= await req.json();
      this.paes= data.paes;
      this.carnes= data.carnes;
      this.opcionaisdata=data.opcionais;
      },
      
      async createBurger(e){
        e.preventDefault();
         const data={
           nome:this.nome,
           carne:this.carne,
           pao:this.pao,
           opcionais:Array.from(this.opcionais),
            status: "solicitado"
         }
         const dataJson= JSON.stringify(data);
         const req= await fetch("http://localhost:3000/burgers",{
            method: "POST",
            headers: {"Content-Type":"application/json"},
            body:dataJson
         });
         const res= await req.json();
          
          //mesaje de suceso
          this.msg=`Pedido Nº ${res.id} realizado exitosamente`

          setTimeout(() => this.msg="",2000)
            
         

          this.nome="";
          this.carne="";
          this.pao="";
          this.opcionais="";

      }
    },
    mounted(){
        this.getIngredientes()
    }
}
</script>
<style scoped>
#burger-form{
    max-width: 400px;
    margin: 0 auto;
}

.input-container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}
label{
    font-weight: bold;
    margin-bottom: 15px;
    color:#222;
    padding: 5px 10px;
   border-left: 4px solid #16eb44 ;
}

input select{
 padding: 5px 10px;
 width: 300px;
    }

.opcion-container{
    flex-direction: row;
    flex-wrap: wrap;
}

#opcione-labe{
    width: 100%;
}
.opcion-container{
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;

}
    .opcion-container span{
        width: auto;
        margin-left: 6px;
        font-weight: bold;
    }

    .opcion-container input{
        width: auto;
    }
.submit-btn{
    background-color: #222;
    color:white;
    font-weight: bold;
    border: 2px solid #222 ;
    font-size: 14px;
    margin: 0 auto;
    cursor: pointer;
    transition: 5s;
    

}
.submit-btn:hover{
    background-color: transparent;
    color:rgb(59, 206, 39)
}
</style>
