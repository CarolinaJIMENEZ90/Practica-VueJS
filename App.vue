<template>
<div>
<NavBar :logo="logo_src" :alt="app_name"/>

<router-view/>
<Footer/>
</div>

</template>

 <script>
 
 import NavBar from './components/NavBar.vue'
 import Footer from './components/Footer.vue'

export default{
  components:{
  NavBar,
  Footer
},
data(){
  return{
    logo_src:"/img/logo.jpg",
    app_name:"Mi Burger"

  }
}
}
 </script>

 <style>
 *{
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  padding: 0;
  margin: 0%;
  box-sizing: border-box;
 }
 .main-container{
  margin: 50px;
  min-height: 250px;
 }
 h1{
  text-align: center;
  font-size: 32px;
  margin-bottom: 30px;
  color:rgb(13, 235, 79)
 }
 </style>