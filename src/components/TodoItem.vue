<template>
  <div class="flex items-center justify-between group p-4 hover:bg-gray-50 rounded-lg transition-colors">
    <div class="flex-1">
      <input
        v-if="todo.isEditing"
        v-model="editableTitle"
        @keyup.enter="saveTodo"
        @blur="saveTodo"
        class="w-full px-2 py-1 border-b focus:outline-none focus:ring-2 focus:ring-blue-500"
      />
      <span v-else :class="{ 'line-through text-gray-400': todo.completed }" @click="toggleComplete"
      class="cursor-pointer">
        {{ todo.title }}
      </span>
    </div>

    <div class="flex gap-2 ml-4">
      <button
        @click="toggleEdit"
        class="p-2 text-blue-500 hover:bg-blue-100 rounded-md transition-colors"
      >
        {{ todo.isEditing ? '💾' : '✏️' }}
      </button>
      <button
        @click="$emit('delete-todo', todo.id)"
        class="p-2 text-red-500 hover:bg-red-100 rounded-md transition-colors"
      >
        🗑️
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
  todo: {
    type: Object,
    required: true
  }
});

const emit = defineEmits(['update-todo', 'delete-todo']);

const editableTitle = ref(props.todo.title);

watch(() => props.todo.title, (newVal) => {
  editableTitle.value = newVal;
});

const toggleEdit = () => {
  if (props.todo.isEditing) {
    saveTodo();
  } else {
    emit('update-todo', { ...props.todo, isEditing: true });
  }
};

const saveTodo = () => {
  const trimmedTitle = editableTitle.value.trim();
  if (!trimmedTitle) {
    emit('delete-todo', props.todo.id);
    return;
  }
  
  emit('update-todo', {
    ...props.todo,
    title: trimmedTitle,
    isEditing: false
  });
};

const toggleComplete = () => {
  emit('update-todo', {
    ...props.todo,
    completed: !props.todo.completed
  });
};
</script>