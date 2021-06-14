<template>
  <div>
    <h2>Vue application!!!</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <AddTodo
        @add-todo="addTodo"
    />
    <TodoList
        v-bind:todos="todos"
        @remove-todo="removeTodo"
    />
  </div>
</template>

<script>

import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'

export default {
  name: 'App',
  data() {
    return {
      todos: [
        {id: 1, title: 'work 1', completed: true},
        {id: 2, title: 'work 2', completed: false},
        {id: 3, title: 'work 3', completed: false},
        {id: 4, title: 'work 4', completed: false},
        {id: 5, title: 'work 5', completed: false}
      ]
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=10')
        .then(response => response.json())
        .then(json => {
          this.todos = json
        })
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t=>t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList,
    AddTodo
  }
}
</script>

<style scoped>

</style>