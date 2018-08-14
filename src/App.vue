<template>
  <div id="app">
    <h1>{{title}}</h1>
    <ul class="todos">
      <li v-for="(todo,index) in todos"
          :class="{'checked':todo.done}"
          :key="index">
        <label for="">{{index+1}}.{{todo.value}}</label>
        <time>{{todo.created}}</time>
      </li>
    </ul>
  </div>
</template>

<script>
import './assets/todo.less'
import './assets/site.less'
export default {
  name: 'app',
  data() {
    return {
      title: 'vue-todo',
      todos: [
        {
          value: 'todo 1',
          done: false,
          created: Date.now()
        },
        {
          value: 'todo 2',
          done: true,
          created: Date.now()
        }
      ]
    }
  }
}
</script>

<style scoped>

</style>
