<script setup>
import { ref } from "vue";


const todoName = ref("")
const todoPrio = ref(null)
const todos = ref([
  { title: "buy milk", prio: 2, complete: false }
  
  
])




function todoAdd() {
  todos.value.push({
    title: todoName.value,
    prio: todoPrio.value,
    complete: false,
    
  })
  
  todoName.value = ""
  todoPrio.value = null
}

 function removeAllTodos() {
      todos.value = [];
    }
/* function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
} */
  function removeTodo(index) {
      todos.value.splice(index, 1);
    }
 function markAsDone(todoIndex) {
  todos.value.forEach((todo, index) => {
    if (index === todoIndex) {
      todo.complete = !todo.complete
    }
    return todo;
  })
  
} 

   
</script>

<template>
  <h1>Todo List</h1>
  

  <div>
    <input v-model="todoName" placeholder="Todo" />
    <input v-model="todoPrio" maxlength="4" pattern="\d{4}" type="number"  required placeholder="prio" />
    <button @click="todoAdd">Add</button>
    
  </div>
  <button @click="removeAllTodos">remove all</button>

  <ul >
    <li class="lista" v-for="(todo, index) in todos" :key="index">
      <span :class="{completed: todo.complete}">
      {{ todo.title }} - prio: {{ todo.prio }}</span>
     
      <button @click="markAsDone(index)">Done</button>

      <button @click="removeTodo(todo)">Delete</button>
    </li>
  </ul>
</template>



<style>
.completed{
  color: grey;
  text-decoration:line-through;
  opacity: 0.6;
}
.lista {list-style-type: none;
margin-top: 5px;
}
button{margin:3px;
opacity: 0.7;}
</style>