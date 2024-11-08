<script setup>
import { ref } from "vue";

// Define todos array and new todo text as reactive variables
const todos = ref([
  {
    id: 1,
    text: "一段文字",
    completed: false,
  },
]);

const text = ref("");

// Function to add a new todo item
const addTodo = () => {
  if (text.value.trim()) {
    todos.value.push({
      text: text.value,
      id: Date.now(),
      completed: false,
    });
    text.value = "";
  }
};

// Function to toggle completion status of a todo
const toggleComplete = (id) => {
  const todo = todos.value.find((todo) => todo.id === id);
  if (todo) {
    todo.completed = !todo.completed;
  }
};

// Function to delete a todo
const deleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};
</script>

<template>
  <div class="max-w-md mx-auto p-4 bg-white rounded-lg shadow-lg">
    <div class="flex items-center space-x-2 mb-4">
      <input 
        type="text" 
        v-model="text" 
        placeholder="新增待辦事項" 
        class="flex-grow px-4 py-2 border border-gray-300 rounded focus:outline-none focus:ring-2 focus:ring-green-500"
      />
      <button @click="addTodo" class="px-4 py-2 bg-green-500 text-white rounded hover:bg-green-600">新增</button>
    </div>
    <hr class="my-4" />

    <div class="flex justify-between space-x-4">
      <div class="w-1/2">
        <h2 class="text-lg font-semibold mb-2">未完成</h2>
        <div v-for="todo in todos" :key="todo.id">
          <template v-if="!todo.completed">
            <div class="flex items-center justify-between bg-gray-100 p-2 mb-2 rounded">
              <span>{{ todo.text }}</span>
              <div class="space-x-2">
                <button @click="toggleComplete(todo.id)" class="px-2 py-1 bg-blue-500 text-white rounded hover:bg-blue-600">完成</button>
                <button @click="deleteTodo(todo.id)" class="px-2 py-1 bg-red-500 text-white rounded hover:bg-red-600">X</button>
              </div>
            </div>
          </template>
        </div>
      </div>

      <div class="w-1/2">
        <h2 class="text-lg font-semibold mb-2">已完成</h2>
        <div v-for="todo in todos" :key="todo.id">
          <template v-if="todo.completed">
            <div class="flex items-center justify-between bg-gray-100 p-2 mb-2 rounded">
              <span class="line-through text-gray-500">{{ todo.text }}</span>
              <div class="space-x-2">
                <button @click="toggleComplete(todo.id)" class="px-2 py-1 bg-yellow-500 text-white rounded hover:bg-yellow-600">未完成</button>
                <button @click="deleteTodo(todo.id)" class="px-2 py-1 bg-red-500 text-white rounded hover:bg-red-600">X</button>
              </div>
            </div>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Scoped style for additional customization if needed */
</style>
