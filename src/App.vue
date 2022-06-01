<template>
  <div class="row">
    <div class="col-sm-3"></div>
    <div class="col-sm-6 bg-secondary text-white">
      <div class="row">
        <div class="col-sm-12 text-center">
          <h1 class="">Unsere Todos</h1>
          <p class="fs-6">
            {{ openTodos.length > 0 ? 'Offenen Todos: ' + openTodos.length : 'Keine Todos!' }}
          </p>
        </div>
      </div>
      <div class="row border-bottom justify-content-center">
        <div class="col-sm-5 pr-1 mb-2">
          <input class="form-control-sm form-control" type="text" v-model="newTodo" id="newTodo" />
        </div>
        <div class="col-sm-2 pl-1 ">
          <button class="btn btn-sm btn-light" @click="addTodo">Add Todo</button>
        </div>
      </div>
      <div class="row" v-for="(todo, index) in todos" :key="todo.todo">
        <Todo :todoprop="todo" :todoindex="index" @toggledone-index="toggleDone" @removeTodo-index="deleteTodo" />
      </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/Todo.vue'

export default {
  name: 'App',
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  methods: {
    toggleDone(index) {
      this.todos[index].done = !this.todos[index].done;
      this.storedTodos();
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
      this.storedTodos();
    },
    addTodo() {
      if (this.newTodo.trim().length > 0) {
        this.todos.push({ todo: this.newTodo, done: false });
        this.newTodo = '';
        this.storedTodos();
      }
    },
    storedTodos() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    }
  },
  mounted() {
    let data = localStorage.getItem('todos');
    if (data !== '' && data !== null) {
      this.todos = JSON.parse(data);
    }else{
      this.todos = [];
    }
  },
  computed: {
    openTodos() {
      let openTodos = this.todos.filter((todo) => {
        return !todo.done;
      });
      return openTodos;
    }
  },
  components: {
    Todo,
  }
}
</script>