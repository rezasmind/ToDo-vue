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
        todos.value.push({
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
  },
  mounted () {
    if (localStorage.getItem('todos')) this.todos = JSON.parse(localStorage.getItem('todos'));
  },
  watch: {
      // watch todos change
      todos: {
          handler () {
              localStorage.setItem('todos', JSON.stringify(this.todos));
          },
          deep: true
    }

  }
}
</script>

<style>
body {
  background: #41B883;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background: #fff;
  border-radius: 12px;
  width: 500px;
  margin: 0 auto;
  margin-top: 0px ;
  display: flex;
  justify-content: center;
  flex-direction: column;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  }

ul {
  padding: 0;
}

.done {
  text-decoration: line-through;
}



form input {
  font-size: 16px;
  border: none;
  border-bottom: 1px solid #ccc;
  background: none;
  color: black;
}

form input::placeholder {
  color: black;
  opacity: 0.8;
}

form input:focus {
  border-bottom: 1px solid #41B883;
}

form button {
  background: none;
  border: 1px solid #ccc;
  color: black;
  font-size: 16px;
  margin: 0px 5px;
  border-radius: 7px;
  padding: 5px 10px;
  cursor: pointer;
  transition: ease-in-out 250ms;
}

form button:hover {
  background: #41B883;
  color: white;
  border: 1px solid #41B883;
  transition: 25ms ease-in-out;

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
  transition: 250ms ease-in-out;
}

li:hover {
  background: #41B883;
  color: white;
  border: 1px solid #41B883;

}

.lidone {
  background: green;
  color : white;
}
</style>
