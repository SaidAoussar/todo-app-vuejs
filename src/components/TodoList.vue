<template>
  <div>
    <div v-if="todos.length > 0" class="space-y-2">
      <TodoItem
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @delete-todo="$emit('delete-todo', $event)"
        @update-todo="$emit('update-todo', $event)"
      />
    </div>
    <div v-else class="text-gray-500 text-center py-4">
      No todos yet. Add your first task!
    </div>
  </div>
</template>

<script setup>
import TodoItem from './TodoItem.vue';

defineProps({
  todos: {
    type: Array,
    required: true
  }
});

defineEmits(['delete-todo', 'update-todo']);
</script>