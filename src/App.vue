<template>
   
  <div id="app">
    <h1>Todo App</h1>
    <form @submit.prevent="addTodo()">
      <label> New ToDo </label>
      <input type="text" v-model="newTodo" placeholder="Add a new todo">
      <button type="submit">Add</button>
    </form>

    <h2>Todo List</h2>
    <ul>
      <li v-for="(todo,index) in todos" :key="index">
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.done {
  text-decoration: line-through;
}

li {
  cursor: pointer;
}
</style>
