<script setup>
import {ref} from 'vue'
let todos = ref([])
let newTodo = ref('')
function addTodo() {
todos.value.push(newTodo.value)
newTodo.value = ""
}
function deleteTodo (index){
alert("deleted")
todos.value.splice(index, 1)

}
</script>

<template>
<body>
  <div>
  <h1>My Todo Application</h1>
  <input v-model="newTodo" @keydown.enter="addTodo">
  &nbsp;
  <button @click="addTodo">Add Task</button>
  <ul>
  <li v-for="(todo, index) in todos">{{ index }} {{ todo }} <button @click="deleteTodo">🚮</button> </li>
  </ul>
</div>
</body>
</template>

<style scoped>
div{

  text-align: center;
}

ul {

  margin-left: 42%;
  margin-right: 45%;
}


body{
  background-color: lightblue;
  border: 100%;

}
</style>
