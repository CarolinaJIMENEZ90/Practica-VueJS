<template>
   <div id="main-baneer">
    <h1>Tu <span>Mejor</span> Burger</h1>
   </div>
</template>


 <script>
export default{
name:"Baneer"
}

 </script>
 
 <style scoped>
 #main-baneer{
    background-image: url(https://i.pinimg.com/736x/b3/e4/a5/b3e4a51b4277fd7e8189601ce15dc673.jpg);
    background-position:  0 -240px;
    background-size: cover;
    height: 550px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
 }
 #main-baneer h1 {
    color:white;
    text-align: center;
    font-size: 40px;
    padding:  40px 20px ;
 }
 </style>