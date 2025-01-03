<template>
  <div>
    <TodoList :activeTodo="activeTodo" :todos="todosList" @deleteTodo="onDeleteTodo" @selectedTodo="onSelectedActiveTodo" @copyTodo="onCopyTodo"/>
    <CreateTodo :editableTodo="editableTodo" @updateTodosList="onUpdatedTodosList"/>
  </div>

</template>

<script setup>
import { computed, ref } from 'vue';
import CreateTodo from './components/CreateTodo.vue';
import TodoList from './components/todoList.vue';
import { v4 as uuidv4 } from 'uuid';

const todosList = ref([])
const activeTodo = ref()

const editableTodo = computed(()=>{
  const todoIndex = todosList.value.findIndex((todo) => {
    return todo.id == activeTodo.value
  })
  return todosList.value[todoIndex]
})

function onUpdatedTodosList(todo) {
  todosList.value.push({
    id: uuidv4(),
    text: todo
  })

}

function onSelectedActiveTodo(id) {
  if(activeTodo.value==id)
  activeTodo.value = null
  else  activeTodo.value = id
}

function onDeleteTodo(id){
  todosList.value = todosList.value.filter((todo) => {
    return todo.id != id
  })
}
function onCopyTodo(id){
  const todoIndex = todosList.value.findIndex((todo) => {
    return todo.id == id
  })
  const todo = todosList.value[todoIndex]
  onUpdatedTodosList(todo.text)
}
</script>