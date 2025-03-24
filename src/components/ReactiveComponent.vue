<script setup>
import { reactive, ref } from "vue";

const reactiveVariable = reactive({ count: 0 });
const reactiveVariable2 = reactive(["ALI","Abdullah", "Umar"]);
const handleChangesInReactive=()=>{
reactiveVariable2[0]  = "usman"
reactiveVariable2[1]  = "amir"
  reactiveVariable2.push("Ali Abdullah Shah Rizvi")
}

const reactiveVariable3 = reactive([ref("Ali"),ref("shanza"),ref("Abdullah")]);



</script>
<template>
  <button class="px-4 bg-green-400 py-2" @click="reactiveVariable.count++">
    {{ reactiveVariable.count }}
  </button>

<h1>{{ reactiveVariable2 }}</h1>

  <button class="px-4 bg-green-400 py-2" @click=" handleChangesInReactive ">
    hit that shit  </button>

    <h1>
{{ reactiveVariable3[0] }}
    </h1>



</template>
