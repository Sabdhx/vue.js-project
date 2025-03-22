<script setup>
 const imageInfo = {
  src:"https://th.bing.com/th/id/OIF.i7Fv8zzMfFvkn67zFDMeyw?w=318&h=180&c=7&r=0&o=5&pid=1.7",
  alt:"image",
  width: "300px",
  height: "200px",

 }


const helloMan = (age, name) => {
  return `This is the person ${name} and this is his age: ${age}`;
  
};

const googleLink = "https://www.google.com";
</script>

<template>
<!-- <img v-bind:="imageInfo"> -->
<h1 class="text-blue-400 text-3xl font-bold">Hey, how are you?</h1>
  <h1>{{ helloMan(23, "Ali") }}</h1>
  <a :href="googleLink" target="_blank" class="text-blue-500 ">
    Google
  </a>
  <h1 class="m-class">hey this is a module class</h1>
 
</template>

<style module>
.m-class{
  background-color: red;
  color:gray
}
</style>