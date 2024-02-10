<template>
  <div id="app">
    <h1>Todo List</h1>

    <!-- Display each todo item using the TodoItem component -->
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @update-todo="handleUpdateTodo"
      @edit-todo="handleEditTodo"
      @delete-todo="handleDeleteTodo"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import TodoItem from './components/TodoItem.vue'

export default defineComponent({
  components: {
    TodoItem
  },
  data() {
    return {
      todos: [
        { id: 1, title: 'Learn Vue.js', completed: false },
        { id: 2, title: 'Build a Todo App', completed: true },
        { id: 3, title: 'Explore Vuex', completed: false }
      ]
    }
  },
  methods: {
    // Handler for updating todo item
    handleUpdateTodo(updatedTodo) {
      const index = this.todos.findIndex((todo) => todo.id === updatedTodo.id)
      if (index !== -1) {
        this.todos.splice(index, 1, updatedTodo)
      }
    },
    // Handler for editing todo item
    handleEditTodo(todo) {
      const editedTitle = prompt('Enter the new title:', todo.title)
      if (editedTitle !== null && editedTitle.trim() !== '') {
        const updatedTodo = { ...todo, title: editedTitle }
        this.handleUpdateTodo(updatedTodo)
      }
    },
    // Handler for deleting todo item
    handleDeleteTodo(todo) {
      const index = this.todos.findIndex((t) => t.id === todo.id)
      if (index !== -1) {
        this.todos.splice(index, 1)
      }
    }
  }
})
</script>

<style>
/* Add your CSS styles here */
</style>
