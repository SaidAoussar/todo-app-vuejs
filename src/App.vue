<template>
  <div class="min-h-screen bg-gray-100 py-8">
    <div class="max-w-md mx-auto bg-white rounded-lg shadow p-6">
      <h1 class="text-2xl font-bold text-gray-800 mb-6">Todo App</h1>
      <AddTodo @add-todo="addTodo" />
      <TodoList
        :todos="todos"
        @delete-todo="deleteTodo"
        @update-todo="updateTodo"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue';
import AddTodo from './components/AddTodo.vue';
import TodoList from './components/TodoList.vue';

const todos = reactive([]);
let idCounter = 0;

const addTodo = (title) => {
  if (title.trim()) {
    todos.push({
      id: idCounter++,
      title: title.trim(),
      completed: false,
      isEditing: false
    });
  }
};

const deleteTodo = (id) => {
  const index = todos.findIndex(todo => todo.id === id);
  todos.splice(index, 1);
};

const updateTodo = (updatedTodo) => {
  const index = todos.findIndex(todo => todo.id === updatedTodo.id);
  todos[index] = updatedTodo;
};
</script>