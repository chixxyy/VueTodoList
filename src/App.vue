<script setup>
import { ref } from "vue";

const todos = ref([
  {
    id: 1,
    text: "一段文字",
    completed: false,
  },
]);

const text = ref("");

const addTodo = () => {
  if (text.value.trim()) {
    todos.value.push({
      text: text.value,
      id: new Date().getTime(),
      completed: false,
    });
    text.value = ""; // 清空輸入框
  }
};

const toggleComplete = (id) => {
  const todo = todos.value.find((todo) => todo.id === id);
  if (todo) {
    todo.completed = !todo.completed;
  }
};

const deleteTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};
</script>

<template>
  <input type="text" v-model="text" placeholder="新增待辦事項" />
  <button @click="addTodo">新增</button>
  <hr />

  <div style="display: flex; justify-content: space-between;">
    <div>
      <h2>未完成</h2>
      <div v-for="todo in todos" :key="todo.id">
        <template v-if="!todo.completed">
          <span>{{ todo.text }}</span>
          <button @click="toggleComplete(todo.id)">完成</button>
          <button @click="deleteTodo(todo.id)">X</button>
        </template>
      </div>
    </div>

    <div>
      <h2>已完成</h2>
      <div v-for="todo in todos" :key="todo.id">
        <template v-if="todo.completed">
          <span :style="{ textDecoration: 'line-through' }">{{ todo.text }}</span>
          <button @click="toggleComplete(todo.id)">未完成</button>
          <button @click="deleteTodo(todo.id)">X</button>
        </template>
      </div>
    </div>
  </div>
</template>
