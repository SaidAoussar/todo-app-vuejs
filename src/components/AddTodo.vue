<template>
  <div class="flex gap-2 mb-6">
    <input
      v-model="newTodo"
      @keyup.enter="handleAddTodo"
      placeholder="Add a new task"
      class="flex-1 px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
    />
    <button
      @click="handleAddTodo"
      class="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 transition-colors"
    >
      Add
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const newTodo = ref('');
const emit = defineEmits(['add-todo']);

const handleAddTodo = () => {
  if (newTodo.value.trim()) {
    emit('add-todo', newTodo.value.trim());
    newTodo.value = '';
  }
};
</script>