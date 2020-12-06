<template>
  <div>
    <h2>Todo list</h2>
<!--    <router-link to="/">Home</router-link>-->
    <hr>
    <AddTodo
      @add-todo="addTodo"
    />
    <hr>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="complited">Complited</option>
      <option value="not-complited">Not complited</option>
    </select>
    <Loader v-if="loading" />
    <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-item="removeItem"
    />
    <p v-else>No todos</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'

export default {
  name: 'App',
  data () {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted () {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json
          this.loading = false
        }, 1000)
      })
  },
  // watch: {
  //   filter (value) {
  //     console.log(value)
  //   }
  // },
  computed: {
    // eslint-disable-next-line vue/return-in-computed-property
    filteredTodos () {
      if (this.filter === 'all') {
        return this.todos
      }

      if (this.filter === 'complited') {
        return this.todos.filter(t => t.completed)
      }

      if (this.filter === 'not-complited') {
        return this.todos.filter(t => !t.completed)
      }
    }
  },
  methods: {
    removeItem (id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo (todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  }
}
</script>

<style scoped>
select {
  margin: 25px 0;
  display: flex;
}
</style>
