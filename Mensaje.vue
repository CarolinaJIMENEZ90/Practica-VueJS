<template>
    <div class="mjs-container">
{{msg}}
    </div>
</template>

<script>
export default{
    name:"Mensaje",
    props:{
        msg:String
    }
}
</script>
<style scoped>
.mjs-container{
    color:rgb(11, 11, 12);
    background-color: rgb(141, 223, 238);
    border: 2px solid #060adb;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
}
</style>