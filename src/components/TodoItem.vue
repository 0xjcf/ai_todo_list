<template>
  <div class="todo-item">
    <!-- Checkbox for marking the todo item as completed -->
    <input type="checkbox" :checked="todo.completed" @change="toggleCompletion" />

    <!-- Display the title of the todo item -->
    <span :class="{ completed: todo.completed }">{{ todo.title }}</span>

    <!-- Buttons for editing and deleting the todo item -->
    <button @click="editTodo">Edit</button>
    <button @click="deleteTodo">Delete</button>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue'

interface Todo {
  id: number
  title: string
  completed: boolean
}

const props = defineProps({
  todo: {
    type: Object as () => Todo,
    required: true
  }
})

const emit = defineEmits(['update-todo', 'edit-todo', 'delete-todo'])

// Method to toggle the completion status of the todo item
const toggleCompletion = () => {
  const updatedTodo = { ...props.todo, completed: !props.todo.completed }
  emit('update-todo', updatedTodo)
}

// Method to edit the todo item
const editTodo = () => {
  emit('edit-todo', props.todo)
}

// Method to delete the todo item
const deleteTodo = () => {
  emit('delete-todo', props.todo)
}
</script>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  margin-bottom: 5px;
}

.completed {
  text-decoration: line-through;
}
</style>
