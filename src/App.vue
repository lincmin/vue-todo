<template>
  <div id="app">
    <h1>{{title}}</h1>
    <ul class="todos">
      <li>
        <input v-model="newTodo"
               @keyup.13="addItem"
               placeholder="输入新增事项"
               autofocus="true">
      </li>
      <li v-for="(todo,index) in todos"
          :class="{'checked':todo.done}"
          :key="index">
        <input type="checkbox"
               @change="saveToStore"
               v-model="todo.done">
        <label for="">{{index+1}}.{{todo.value}}</label>
        <time>{{todo.created | date}}</time>
        <button @click.prevent="delItem(todo)"></button>
      </li>
    </ul>
  </div>
</template>

<script>
import './assets/todo.less'
import './assets/site.less'
import moment from 'moment'
import 'moment/locale/zh-cn'
moment.locale('zh-cn')
export default {
  name: 'app',
  data() {
    return {
      title: 'vue-todo',
      newTodo: '',
      todos: []
    }
  },
  created() {
    if (this.is_initialized) {
      this.todos = JSON.parse(localStorage.getItem('VUE-TODO'))
    }
  },
  computed: {
    is_initialized() {
      return localStorage.getItem('VUE-TODO') != null
    }
  },
  filters: {
    date(val) {
      return moment(val).calendar()
    }
  },
  methods: {
    addItem() {
      this.todos.push({
        value: this.newTodo,
        created: Date.now(),
        done: false
      })
      this.saveToStore()
    },
    delItem(todo) {
      this.todos = this.todos.filter((x) => x !== todo)
      this.saveToStore()
    },
    saveToStore() {
      localStorage.setItem('VUE-TODO', JSON.stringify(this.todos))
    }
  }
}
</script>

<style scoped>

</style>
