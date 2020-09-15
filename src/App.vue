<template>
  <div id="app">
    <h1>To-DO Application!</h1>
    <addTodo
        @add-todo="addTodo"
    />
    <hr>
    <ToDoList
    v-bind:todos = "todos"
    @remove-todo = "removeTodo"
    />
  </div>
</template>

<script>
import ToDoList from '@/components/toDoList'
import addTodo from '@/components/addTodo'
export default {
  name: 'App',
  data() {
    return {
      todos: [
        {id: 1, title: 'Купить хлеб', completed: false},
        {id: 2, title: 'Купить масло', completed: false},
        {id: 3, title: 'Купить яйца', completed: false},
      ]
    }
  },
  components: {
    ToDoList,
    addTodo
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

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
