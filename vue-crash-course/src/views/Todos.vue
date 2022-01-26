<template>
<h2>Todo app</h2>
<AddTodo @add-todo="addTodo" />
<select v-model="filter">
    <option value="all">All</option>
    <option value="completed">Completed</option>
    <option value="not-completed">Not Completed</option>
</select>
<router-link to="/">Home</router-link>
<Loader v-if="loading" />
<TodoList 
  v-else-if="todos.length"
  v-bind:todos="filteredTodos" 
  @remove-todo="removeTodo"
/>
<p v-else>No todos!</p>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'
export default {
  name: 'App',
  components: {
    TodoList,
    AddTodo,
    Loader
  },
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
          this.todos = json;
          this.loading = false;
       })
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  computed: {
      filteredTodos() {
          if (this.filter === 'all') {
              return this.todos
          }

          if (this.filter === 'completed') {
              return this.todos.filter(t => t.computed)
          }

          if (this.filter === 'not-completed') {
              return this.todos.filter(t => t.computed)
          }
      }
  }
//   watch: {
//       filter(value) {
//           console.log(value)
//       }
//   }
}
</script>