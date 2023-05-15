<script setup>
import {ref, watch} from 'vue'
let todos = ref(JSON.parse(window.localStorage.getItem('todos')))
let newTodo = ref('')
let input = ref('')
watch(todos, function(value){window.localStorage.setItem('todos' ,JSON.stringify(value))},{deep:true})
function addTodo() {
todos.value.push({text:newTodo.value, complete:false})
newTodo.value = ""
}
function deleteTodo (index){
todos.value.splice(index, 1) }
</script>

<template>
<body>
  
  <h1>My Todo Application</h1>
  <hr>
  <input v-model="newTodo" @keydown.enter="addTodo">
  &nbsp;
  <button @click="addTodo">Add Task</button>
  <ul>
  <li v-for="(todo, index) in todos" style="text-align: left;" ><input type="checkbox" v-model="todo.complete" class="checkmark  " style="margin-bottom:0;">
    {{ todo.text }} 
    <button @click="deleteTodo(index)">🚮</button>  <hr style="color: blanchedalmond;,width: 2px;"> </li>
  </ul>

</body>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@300&display=swap');

div{
  width: 500px;
  text-align: center;
}

ul {

  margin-left: 39%;
  margin-right: 45%;
}


body{
  
  background-color: lightblue;
  text-align: center;
  height: 1080px;
  font-family: 'Inconsolata', monospace;

}


/* Customize the label (the container) */
.container {
  display: table;

  padding-left: 35px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  display: inline;
  text-align: left;
  height: 22px;
  width: 22px;
  background-color: #eee;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #000;
}

/* Create the checkmark/indicator (hidden when not checked) */


/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}



</style>
