<script setup lang="ts">
import { ref } from 'vue';
import type { ITodo } from './interface/todoInterface';

const newTask = ref<string>("")

const todos = ref<ITodo[]>([
  {
    id:1,
    task:"badminton",
    isCompleted: false,
    isEditing: false
  },
  {
    id:2,
    task:"basketball",
    isCompleted: false,
    isEditing: false
  },
  {
    id:3,
    task:"volleyball",
    isCompleted: false,
    isEditing: false
  },
])

function addTodo() {
  todos.value = [{id: Math.random(), task: newTask.value, isCompleted: false, isEditing: false}, ...todos.value];
}

function removeTodo(id: number) {
  todos.value = todos.value.filter((item) => item.id !== id)
}

function toggleComplete(todo: ITodo) {
  todo.isCompleted = !todo.isCompleted
}

function toggleEdit(todo: ITodo) {
  todo.isEditing = !todo.isEditing 
}
</script>

<template>
  <main>
    <h1>Vuets Crud App</h1>

    <input type="text" v-model="newTask">
    <button @click.prevent="addTodo">Add</button>
    
    <div v-for="todo in todos" key="todo.id">
      
      <h2 v-if="todo.isEditing === false">{{todo.task}}</h2>
      
      <button @click.prevent="removeTodo(todo.id)">Remove</button>

      <button @click.prevent="toggleComplete(todo)">complete</button>

        <div v-if="todo.isEditing === true">
          <input type="text" v-model="todo.task" @keyup.enter="toggleEdit(todo)">
          <button @click.prevent="toggleEdit(todo)">Done edit</button>
        </div>

        <button v-if="todo.isEditing === false" @click.prevent="toggleEdit(todo)">Edit</button>

    </div>
  </main>
</template>