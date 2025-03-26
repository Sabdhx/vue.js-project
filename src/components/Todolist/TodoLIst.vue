<script setup>
import { ref } from "vue";

const inputValue = ref("");
const data = ref([]); // List of tasks
const completed = ref([]); // Completed tasks
const editIndex = ref(null);
const editInput = ref("");
const isOpen = ref(false);

const addNewData = () => {
  if (!inputValue.value.trim()) return; // Prevent adding empty values
  data.value.push({ text: inputValue.value, done: false }); // Store as an object
  inputValue.value = "";
};

const handleDelete = (i) => {
  data.value.splice(i, 1);
};

const handleEditInput = (event, index) => {
  data.value[index].text = event.target.value;
};

const handleCheck = (index) => {
  const item = data.value[index];
  item.done = !item.done; // Toggle done status

  if (item.done) {
    completed.value.push(item); // Move to completed
    data.value.splice(index, 1); // Remove from main list
  }
};

const removeCompleted = (index) => {
  completed.value.splice(index, 1);
};
</script>

<template>
  <div class="flex justify-center min-h-screen items-center bg-gray-100 p-6">
    <div class="w-full max-w-lg bg-white shadow-lg rounded-lg p-6">
      <h1 class="text-2xl font-semibold text-gray-700 text-center mb-4">
        Todo List
      </h1>

      <!-- Input & Add Button -->
      <div class="flex gap-2">
        <input
          type="text"
          v-model="inputValue"
          placeholder="Enter a todo..."
          class="w-full p-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-400"
          :disabled="isOpen"
        />
        <button
          class="bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600 transition"
          @click="addNewData"
        >
          Add
        </button>
      </div>

      <!-- Todo List -->
      <ul class="mt-4 space-y-3">
        <li
          v-for="(item, index) in data"
          :key="index"
          class="flex justify-between items-center bg-gray-50 p-3 rounded-md shadow-sm border"
        >
          <!-- Task Text with Strike-through for Checked Items -->
          <span
            v-if="editIndex !== index"
            :class="{ 'line-through text-gray-500': item.done }"
          >
            {{ item.text }}
          </span>

          <!-- Edit Input -->
          <input
            v-else
            type="text"
            v-model="editInput"
            class="p-1 border border-gray-300 rounded-md w-full focus:ring-2 focus:ring-blue-400"
            @input="handleEditInput($event, index)"
          />

          <!-- Buttons -->
          <div class="flex gap-2">
            <button
              @click="
                editIndex = index;
                editInput = item.text;
                isOpen = true;
              "
              class="text-blue-500 hover:text-blue-600 transition"
            >
              ✏️
            </button>
            <button
              @click="handleDelete(index)"
              class="text-red-500 hover:text-red-600 transition"
            >
              🗑️
            </button>
            <button
              v-if="editIndex === index"
              @click="editIndex = null; isOpen = false"
              class="text-green-500 hover:text-green-600 transition"
            >
              ✅
            </button>

            <input
              type="checkbox"
              :checked="item.done"
              @change="handleCheck(index)"
              class="w-5 h-5 accent-green-500"
            />
          </div>
        </li>
      </ul>

      <!-- Completed Tasks Section -->
      <h2 v-if="completed.length" class="text-xl font-semibold text-gray-700 mt-6">
        Completed Tasks
      </h2>
      <ul v-if="completed.length" class="mt-2 space-y-3">
        <li
          v-for="(item, index) in completed"
          :key="index"
          class="flex justify-between items-center bg-green-50 p-3 rounded-md shadow-sm border"
        >
          <span class="text-gray-700">{{ item.text }}</span>
          <button
            @click="removeCompleted(index)"
            class="text-red-500 hover:text-red-600 transition"
          >
            ❌
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>
