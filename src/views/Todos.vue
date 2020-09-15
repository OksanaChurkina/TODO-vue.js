<template>
  <div>
    <h2>To-DO Application!</h2>
    <router-link to="/">Home</router-link>
    <addTodo
        @add-todo="addTodo"
    />
    <hr>
    <Loader v-if="loading"/>
    <ToDoList
        v-else-if="todos.length"
        v-bind:todos = "todos"
        @remove-todo = "removeTodo"
    />
    <p v-else>No todos</p>
  </div>
</template>

<script>
import ToDoList from '@/components/toDoList'
import addTodo from '@/components/addTodo'
import Loader from '@/components/Loader'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => {
          setTimeout(() =>{
            this.todos = json
            this.loading = false
          }, 1000)

        })
  },
  components: {
    ToDoList,
    addTodo,
    Loader
  },
  methods: {
    removeTodo(id){
      this.todos = this.todos.filter(t=> t.id !==id)
    },
    addTodo(todo){
      this.todos.push(todo)
    }
  }
}
</script>