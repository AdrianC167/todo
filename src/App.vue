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

function activeFilter (todo) {
  return todo.complete == false

}


</script>

<template>

  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
    integrity="sha512-iecdLmaskl7CVkqkXNQ/ZH/XLlvWZOJyj7Yy7tcenmpD1ypASozpmT/E0iPtmFIB46ZmdtAc9eNBvH0H/ZpiBw=="
    crossorigin="anonymous" referrerpolicy="no-referrer" />

  <h1>My Todo Application</h1>
  <hr> 

  
  <div v-if="todos.length > 0">
  <input name="filter" type="radio" value="all" v-model="filter" class="radio"> <label>All</label>
  <input name="filter" type="radio" value="active" v-model="filter" class="radio"> <label>Active</label>
  <input name="filter" type="radio" value="completed" v-model="filter" class="radio"> <label>Completed</label>
  </div> 
  <p> {{ todos.filter(activeFilter).length }} items left</p>
 <input v-model="newTodo" @keydown.enter="addTodo" id="textarea" placeholder="Enter Here(You can hit enter when you're done)" style="margin-bottom: 12px;">
  &nbsp;
 
  <button @click="addTodo" style="height: 30px;border-radius: 5%;" class="hover">Add Task</button>


    <ul>
    <div class="wrapper">
      <TransitionGroup name="list" tag="ul">
      <li v-for="(todo, index) in todos.filter(todoFilter)" :key="item" style="text-align: left;" class="animate__bounceIn">
        <input type="checkbox" v-model="todo.complete" id="checkbox" style="margin-bottom:0;" class="radio">
        <label :class="{ completed: todo.complete }"> {{ todo.text }} </label>
        <button @click="deleteTodo(index)" class="right">🚮</button>
            </li>
</TransitionGroup>
    </div> 
  </ul>

 
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@300&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inconsolata:wght@300&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Shadows+Into+Light&display=swap');

h1 {
  font-family: 'Shadows Into Light', cursive;
  text-transform: uppercase;
  font-weight: bolder;
}

p {
  font-family: 'Inconsolata', monospace;

}


li {
  display:flex;
  border-color: rgba(185, 30, 236, 0.923);
  border-width: 1px;
  border-style: ridge;
  height: 45px;
  justify-content: left;
  align-items: center;
  background-color: rgba(110, 167, 117, 0.463);
  transform: scale(1);
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
  transition: 500ms;


}

.wrapper {
  display: block;
  height: 500px;
  position: relative;
  margin: 0px;
  width: 600px;
  top: 0;
  bottom:0;
  left: 0;
  right: 0;
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
  opacity: 100%;
  transition:500ms;

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
width:300px;
text-align: left;

}

#textarea {
height: 25px;
width: 300px;

}

.right{
display: none;
position: absolute;
margin-left: 94%;
align-items: right;
justify-content: right;
text-align: right;
}

li:hover > button {
display:flex;




}


.list-enter-active,
.list-leave-active {
  transition: all .85s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(-150px);
}

.hover:hover{
background-color: lightcyan;

}

</style>
