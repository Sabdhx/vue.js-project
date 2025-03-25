<script setup>
import { ref } from "vue";
import CardTodo from "../CardTodo.vue";

const inputValue = ref("");
const data = ref([]);
const editIndex = ref(null);
const editInput = ref("");

const addNewData = () => {
  data.value.push({ text: inputValue.value, done: false });
  inputValue.value = "";
};

const handleDelete = (index) => {
  data.value.splice(index, 1);

};

const handleEdit = (index, text) => {
  editIndex.value = index;
  editInput.value = text;
};

const saveEdit = (index) => {
  if (!editInput.value.trim()) return;

  data.value[index].text = editInput.value;
  editIndex.value = null;
  editInput.value = "";
};

const toggleTask = (index) => {
  data.value[index].done = !data.value[index].done;
};
</script>

<template>
  <div class="flex justify-center min-h-screen items-center bg-gray-100 p-6">
    <div class="w-full max-w-lg bg-white shadow-lg rounded-lg p-6">
      <h1 class="text-2xl font-semibold text-gray-700 text-center mb-4">
        Todo List
      </h1>

      <div class="flex gap-2">
        <input
          type="text"
          v-model="inputValue"
          placeholder="Enter a todo..."
          class="w-full p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-400"
        />
        <button
          class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 transition"
          @click="addNewData"
        >
          Add
        </button>
      </div>

      <ul class="mt-4 space-y-3">
        <CardTodo
          v-for="(item, index) in data"
          :key="index"
          :item="item"
          :index="index"
          :editIndex="editIndex"
          :editInput="editInput"
          @delete="handleDelete"
          @edit="handleEdit"
          @saveEdit="saveEdit"
          @toggle="toggleTask"
        />
      </ul>
    </div>
  </div>
</template>
