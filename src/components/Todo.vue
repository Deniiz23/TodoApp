<template>
  <div class="col-sm-12 d-flex justify-content-between align-items-center" :class="{'bg-success': this.todo.done, 'bg-danger': !this.todo.done}" @click="toggleTodo">
    <p class="" >{{ todo.todo }}</p>
    <button class="btn btn-sm btn-dark" @click="removeTodo">Delete</button>
  </div>
</template>

<script>
export default {
  name: 'TodoComp',
  props: [
    'todoprop',
    'todoindex'
  ]
  , data() {
    return {
      todo: this.todoprop
    }
  },
  methods: {
    toggleTodo(){
      this.$emit('toggledone-index', this.todoindex);
    },
    removeTodo(){
      this.$emit('removeTodo-index', this.todoindex);
    }
  }
}
</script>