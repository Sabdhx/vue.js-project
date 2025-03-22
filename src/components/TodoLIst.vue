<script setup>
import { ref } from "vue";

const count1 = ref(0);
const count2 = ref(0);
const reactiveConst = reactive
const increment = () => {
  return count1.value++;
};
const decrement = () => {
  return count2.value--;
};



</script>
<template>
  <h1>

        <button
          class="bg-blue-300 py-1 px-5 rounded mx-3 "
          @:click="increment"
        >
          {{count1}}
        </button>
    


         

    <button 
    class="bg-blue-300 py-1 px-5 rounded mx-3 "
   @:click="decrement"
    >{{ count2 }}</button>
  </h1>
</template>
