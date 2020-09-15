<template>
  <div>
    <h2>To-DO Application!</h2>
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
      todos: []
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
        .then(response => response.json())
        .then(json => {
          this.todos = json
        })
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