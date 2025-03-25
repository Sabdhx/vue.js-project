<script setup>
import { defineProps, defineEmits } from "vue";

// Define props
const props = defineProps({
  index: Number,
  item: Object,
  editIndex: Number,
  editInput: String,
});

// Emit events to the parent
const emit = defineEmits(["delete", "edit", "toggle", "saveEdit"]);

const handleDelete = () => {
  emit("delete", props.index);
};

const handleEditInput = (event) => {
  emit("edit", props.index, event.target.value);
};

const saveEdit = () => {
  emit("saveEdit", props.index);
};

const handleCheck = () => {
  emit("toggle", props.index);
};
</script>

<template>
  <li class="flex justify-between items-center bg-gray-50 p-3 rounded-md shadow-sm border w-full">
    <!-- Task Text with Strike-through -->
    <template v-if="editIndex !== index">
      <span :class="{ 'line-through text-gray-500': item.done }">
        {{ item.text }}
      </span>
    </template>

    <!-- Edit Input -->
    <template v-else>
      <input
        type="text"
        :value="editInput"
        class="p-1 border border-gray-300 rounded-md w-full focus:ring-2 focus:ring-blue-400"
        @input="handleEditInput"
      />
    </template>

    <!-- Buttons -->
    <div class="flex gap-2">
      <button
        @click="emit('edit', index, item.text)"
        class="text-blue-500 hover:text-blue-600 transition"
      >
        ✏️
      </button>

      <button @click="handleDelete" class="text-red-500 hover:text-red-600 transition">
        🗑️
      </button>

      <button
        v-if="editIndex === index"
        @click="saveEdit"
        class="text-green-500 hover:text-green-600 transition"
      >
        ✅
      </button>

      <input
        type="checkbox"
        :checked="item.done"
        @change="handleCheck"
        class="w-5 h-5 accent-green-500"
      />
    </div>
  </li>
</template>
