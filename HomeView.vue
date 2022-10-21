<template>

 <div  class="main-container">
  <Banner/>
<h1> Escoja su Burger</h1>
<FormBurger/>
<form action="">

</form>
  </div>
</template>

<script>
 import Banner from "../components/Baneer.vue"
 import FormBurger from "../components/FormBurger.vue"

 export default{
  components:{
    Banner,
    FormBurger
  }
 }
</script>
