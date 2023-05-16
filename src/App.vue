<script setup>
import {ref, watch} from 'vue'
let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
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


  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" integrity="sha512-iecdLmaskl7CVkqkXNQ/ZH/XLlvWZOJyj7Yy7tcenmpD1ypASozpmT/E0iPtmFIB46ZmdtAc9eNBvH0H/ZpiBw==" crossorigin="anonymous" referrerpolicy="no-referrer" />
  <h1>My Todo Application</h1>
  <hr>
  <input v-model="newTodo" @keydown.enter="addTodo">
  &nbsp;
  <button @click="addTodo">Add Task</button>
  <ul>
  <div class="wrapper">
  <li v-for="(todo, index) in todos" style="text-align: left;" :class="{completed: todo.complete}"><input type="checkbox" v-model="todo.complete"  id="checkbox" style="margin-bottom:0;">
   <label> {{ todo.text }} </label>
    <button @click="deleteTodo(index)">🚮</button>  <hr style="color: blanchedalmond;,width: 2px;"> </li> </div>
  </ul>

</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@300&display=swap');






body{
  
  background-color: lightblue;
  text-align: center;
  height: 1080px;
  font-family: 'Inconsolata', monospace;

}


.completed {

text-decoration: line-through;
opacity: 40%;
font-weight: light;


}

.wrapper {

  height: 580px;
  position: absolute;
  margin: auto;
  width: 1000px;
  top: 0;
  bottom: 0;
  left: 0;
  right:0;
  align-items: center;
  justify-content: space-around;


}

input[type="checkbox"]{
  appearance: none;
  -webkit-appearance: none;
  height: 30px;
  width: 30px;
  background-color: #d5d5d5;
  border-radius: 50%;
  cursor: pointer;
 display: flex;
  align-items: center;
  justify-content: center;

}

label {
  color: #4c4c4c;
  font-size: 55px;
  font-family: 'Poppins', sans-serif;
  font-weight: 600;
  cursor: pointer;

}

input[type='checkbox']:after{
  font-family: "Font Awesome 5 Free";
  font-weight: 900;
  content: "\f00c";
  font-size: 20px;
  color: mediumorchid;
  /* display: none; */



}

input[type="checkbox"]:hover{
  background-color: #a5a5a5;

}

input[type="checkbox"]:checked{
background-color: #5bcd3e;

}

input[type="checkbox"]:checkbox:after{
display: block;


}
</style>
