<script setup>
const count = ref(0)
import { ref } from 'vue';
import yelloWorld from './yelloWorld.vue';
const incrementCount=()=>{
  count.value++
}
</script>

<template>
 <h1>
  {{ count }}
 </h1> 
<yelloWorld :count="count" @incrementCount="incrementCount" />
</template>