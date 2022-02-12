<template>
   
  <div id="app">
    <h1>Todo App</h1>
    <form @submit.prevent="addTodo()">
      <input type="text" v-model="newTodo" placeholder="Add a new todo">
      <button type="submit">Add</button>
    </form>

    <h2>Todo List</h2>
    <ul>
      <li v-for="(todo,index) in todos" :key="index" :class="{lidone: todo.done}">
        <span :class="{done: todo.done}" @click="doneToDo(todo)">
          {{ todo.content}}
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
import {ref} from 'vue'


export default {
  name: 'App',
  setup () {
    const newTodo = ref('')
    const defaultData = [{
      done: false,
      content: 'Learn Vue'
    }]
    const todosData = ref(defaultData)
    const todos = ref(todosData)
    function addTodo() {
      if (newTodo.value) {
        todosData.value.push({
          done: false,
          content: newTodo.value
        })
        newTodo.value = ''
      }

    }
    function doneToDo(todo) {
      todo.done = !todo.done
    }
    return {
      newTodo,
      todos,
      addTodo,
      doneToDo
    }
  }
}
</script>

<style>
body {
  background: #2c3e50;
  display: flex;
  justify-content: center;
  align-items: center;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: flex;
  justify-content: center;
  flex-direction: column;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
  margin-top: 60px;
}

.done {
  text-decoration: line-through;
}



form input {
  font-size: 16px;
  border: none;
  border-bottom: 1px solid #ccc;
  background: none;
  color: white;
}

form input::placeholder {
  color: #ccc;
  opacity: 0.8;
}

form button {
  background: none;
  border: 1px solid #ccc;
  color: white;
  font-size: 16px;
  margin: 0px 5px;
  border-radius: 7px;
  padding: 5px 10px;
  cursor: pointer;
}

form button:hover {
  background:white;
  color: #2c3e50;
}

li {
  cursor: pointer;
  text-decoration: none;
  list-style-type: none;
  width: auto;
  margin: 7px;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 10px;
}

.lidone {
  background: green;
  color : white;
}
</style>
