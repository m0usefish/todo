<template>
    <div>
      <div style="display: flex;" v-for="todo in todos" :key="todo.id">
        <p :class="activeTodo == todo.id ? 'activeTodo' : ''" @click = "onTodoSelected(todo.id)">
            {{ todo.text }}
        </p>
        <button @click ="deleteTodo(todo.id)">DELETE</button>
        <button @click="copyTodo(todo.id)">Copy</button>
      </div>
    </div>
</template>

<script setup>

const { todos, activeTodo } = defineProps(['todos', 'activeTodo'])
const emit = defineEmits(['selectedTodo', 'deleteTodo', 'copyTodo'])

function copyTodo(id) {
    emit('copyTodo', id)
}
function deleteTodo(id) {
    emit('deleteTodo', id)
}
function onTodoSelected(id) {
    emit('selectedTodo', id)
}
</script>

<style>
@import '../assets/styles/todoList.css'
</style>