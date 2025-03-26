<script setup>
const props = defineProps({
  count: Number,
  incrementCount:Function
});

const emit = defineEmits(["incrementCount"])

const emiting= ()=>{
  emit("incrementCount")
  emit("incrementCount")
  emit("incrementCount")
  emit("incrementCount")
  emit("incrementCount")
  emit("incrementCount")
}

</script>



<template>
  <button @click="emiting">add</button>
</template>