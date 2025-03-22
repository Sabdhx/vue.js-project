<script setup>
import HelloWorld from "./components/HelloWorld.vue" 
const helloMan=(age,name)=>{
 return `this is the person ${name} and this is his ${age}`
}
</script>

<template>
  <h1 class="text-blue-400 text-3xl font-bold" >hey how r u</h1>
 <h1>{{ helloMan(23,"ALi") }}</h1> 
<HelloWorld/>
</template>

<style scoped>

</style>
