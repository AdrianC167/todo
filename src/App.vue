<script setup>
import { ref, watch } from 'vue'
let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
let newTodo = ref('')
let input = ref('')
let filter = ref("all")

watch(todos, function (value) { window.localStorage.setItem('todos', JSON.stringify(value)) }, { deep: true })
function addTodo() {
  todos.value.push({ text: newTodo.value, complete: false })
  newTodo.value = ""
}
function deleteTodo(index) {
  todos.value.splice(index, 1)
}
function todoFilter(todo) { 
  if (filter.value == 'active') { 
    return todo.complete == false 
  }else if (filter.value == 'completed') {
    return todo.complete == true
  }
     else { 
      return true 
    } 
  }

function deleteAll() {
  windows.localStorage.clear();

}
</script>

<template>

  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
    integrity="sha512-iecdLmaskl7CVkqkXNQ/ZH/XLlvWZOJyj7Yy7tcenmpD1ypASozpmT/E0iPtmFIB46ZmdtAc9eNBvH0H/ZpiBw=="
    crossorigin="anonymous" referrerpolicy="no-referrer" />

  <h1>My Todo Application</h1>
  <hr>
  <input v-model="newTodo" @keydown.enter="addTodo" id="textarea" placeholder="Type Here">
  <input name="filter" type="radio" value="all" v-model="filter" class="radio"> <label>All</label>
  <input name="filter" type="radio" value="active" v-model="filter" class="radio"> <label>Active</label>
  <input name="filter" type="radio" value="completed" v-model="filter" class="radio"> <label>Completed</label>
  &nbsp;
  <button @click="addTodo">Add Task</button>
  <button @click="deleteAll(value)">Delete All</button>
  <ul>
    <div class="wrapper">
      <li v-for="(todo, index) in todos.filter(todoFilter)" style="text-align: left;" >
        <input type="checkbox" v-model="todo.complete" id="checkbox" style="margin-bottom:0;" class="radio">
        <label :class="{ completed: todo.complete }"> {{ todo.text }} </label>
        <button @click="deleteTodo(index)">🚮</button>
     
      </li>
    </div>
  </ul>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@300&display=swap');

li {
  display:flex;
  margin-bottom: 5px;
  margin-top: 5px;
}

ul{
  margin: 0;
  padding: 0px;

}

body {

  background-color: lightblue;
  text-align: center;
  height: 1080px;
  font-family: 'Inconsolata', monospace;

}


.completed {
  display: flex;
  text-decoration: line-through;
  opacity: 40%;
  font-weight: light;


}

.wrapper {
 
  height: 500px;
  position: relative;
  margin: 0px;
  width: 1000px;
  top: 0;
  bottom:0;
  left: 0;
  right: 0;
  align-items: left;
  justify-content: space-around;
  text-align: left;


}


input[type="checkbox"] {
  appearance: none;
  -webkit-appearance: none;
  height: 30px;
  width: 30px;
  background-color: #c3b9b9;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;

}

label {
  color: #4c4c4c;
  font-size: 20px;
  font-family: 'Poppins', sans-serif;
  font-weight: 600;
  cursor: pointer;


}



input[type='checkbox']:after {
  font-family: "Font Awesome 5 Free";
  font-weight: 900;
  content: "\f00c";
  font-size: 20px;
  color: mediumorchid;
  display: none;



}

input[type="checkbox"]:hover {
  background-color: #586066;

}

input[type="checkbox"]:checked {
  background-color: #50c931;

}

input[type="checkbox"]:checked:after {
  display: block;
  text-decoration: none;

}
.radio {
  font-family: 'Inconsolata', monospace;

}

div {

text-align: left;

}

#textarea {
height: 25px;
width: 300px;

}

</style>
