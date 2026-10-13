<script>
export default {
  // Component data and methods
  data() {
    return {
      newTodo: '',
      todos: [],
    }
  },

  // Computed properties for filtering todos by status
  computed: {
    todoItems() {
      return this.todos.filter((todo) => todo.status === 'todo')
    },
    inWorkItems() {
      return this.todos.filter((todo) => todo.status === 'inWork')
    },
    doneItems() {
      return this.todos.filter((todo) => todo.status === 'done')
    },
  },
  // Methods for adding and moving todos
  methods: {
    addTodo() {
      if (this.newTodo.trim() === '') return
      this.todos.push({
        id: Date.now(),
        text: this.newTodo,
        status: 'todo',
      })
      this.newTodo = ''
    },
    moveTodo(todo, newStatus) {
      todo.status = newStatus
    },
  },
}
</script>

<template>
  <!-- Todo List Application -->
  <div>
    <h1>Todo List</h1>
    <!-- Input for adding new todos -->
    <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a todo" />
    <button @click="addTodo">Add</button>

    <!-- Todo column for items with status 'todo' -->
    <div class="todo-list__column">
      <h3>Todo</h3>
      <p>Number of todos: {{ todoItems.length }}</p>
      <ul>
        <li class="todo-list__item" v-for="todo in todoItems" :key="todo.id">
          {{ todo.text }}
          <button @click="moveTodo(todo, 'inWork')">Start</button>
        </li>
      </ul>
    </div>

    <!-- Todo column for items with status 'inWork' -->
    <div class="todo-list__column">
      <h3>In Work</h3>
      <p>Number of todos: {{ inWorkItems.length }}</p>
      <ul>
        <li class="todo-list__item" v-for="todo in inWorkItems" :key="todo.id">
          {{ todo.text }}
          <button @click="moveTodo(todo, 'done')">Finish</button>
        </li>
      </ul>
    </div>

    <!-- Todo column for items with status 'done' -->
    <div class="todo-list__column">
      <h3>Done</h3>
      <p>Number of todos: {{ doneItems.length }}</p>
      <ul>
        <li class="todo-list__item" v-for="todo in doneItems" :key="todo.id">
          {{ todo.text }}
        </li>
      </ul>
    </div>
  </div>
</template>
