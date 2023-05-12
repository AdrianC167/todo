<script setup>
import {ref} from 'vue'
let todos = ref(["a","b","c"])
let newTodo = ref('')
function addTodo() {
todos.value.push({text:newTodo.value, complete:false})
newTodo.value = ""
}
function deleteTodo (index){
alert("deleted")
todos.value.splice(index, 1)

}
</script>

<template>
<body>
  
  <h1>My Todo Application</h1>
  <hr>
  <input v-model="newTodo" @keydown.enter="addTodo">
  &nbsp;
  <button @click="addTodo">Add Task</button>
  <ul>
  <li v-for="(todo, index) in todos"><input type="checkbox" v-model="todo.complete">
    {{ todo.text }} 
    <button @click="deleteTodo(index)">🚮</button> </li>
  </ul>

</body>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@300&display=swap');

div{

  text-align: center;
}

ul {

  margin-left: 42%;
  margin-right: 45%;
}


body{

  background-color: lightblue;
  text-align: center;
  height: 1080px;
  font-family: 'Inconsolata', monospace;

}


</style>
