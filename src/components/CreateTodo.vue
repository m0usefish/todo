<template>
    <div>
        <input v-model="inputValue" type="text">
        <button @click="saveTodo" >Add</button>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const { editableTodo } = defineProps(['editableTodo'])
const emit = defineEmits(['updateTodosList'])

const inputValue = ref('')

function saveTodo() {
    emit('updateTodosList', inputValue.value )

    inputValue.value = ''
}
</script>

<style>
@import '../assets/styles/createTodo.css';
</style>

