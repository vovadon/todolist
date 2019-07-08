<template>
  <div id="app">
    <SearchTodo v-on:change="queryHandler" />
    <div class="page-wrap">
      <AddTodo v-on:add-todo="addTodo" v-bind:isListEmpty="isListEmpty"/>
      <Todos v-if="filtredTodos.length > 0" v-bind:todos="filtredTodos" v-on:del-todo="deleteTodo" />
      <Todos v-else v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    </div>
    <div class="empty-msg" v-if="isListEmpty">Список пуст</div>
  </div>
</template>

<script>
import SearchTodo from './components/SearchTodo.vue'
import AddTodo from './components/AddTodo.vue'
import Todos from './components/Todos.vue'

export default {
  name: 'app',
  components: {
    SearchTodo,
    AddTodo,
    Todos
  },
  data() {
    return {
      todos: [],
      filtredTodos: [],
      lastQuery: '',
      isListEmpty: true
    }
  },
  mounted() {
    if (localStorage.getItem('todos')) {
      try {
        let obj = JSON.parse(localStorage.getItem('todos'));
        this.todos = Object.values(obj);
        this.isListEmpty = this.todos.length > 0 ? false : true;
      }
      catch(e) {
        localStorage.removeItem('todos');
      }
    }
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
      if (this.filtredTodos.length > 0) {
        this.filtredTodos = this.filtredTodos.filter(todo => todo.id !== id);
      }
      this.saveElement();
      if (this.todos.length === 0) {
        this.isListEmpty = true;
      }
    },
    addTodo(newTodo) {
      this.todos.push(newTodo);
      this.saveElement();
      this.queryHandler(this.lastQuery);
      if (this.todos.length > 0) {
        this.isListEmpty = false;
      }
    },
    queryHandler(query) {
      this.lastQuery = query;
      this.filtredTodos = this.todos.filter(todo => todo.title.toLowerCase().includes(query.toLowerCase()));
    },
    saveElement() {
      const parsed = JSON.stringify(this.todos);
      localStorage.setItem('todos', parsed);
    },
  }
}
</script>

<style>
html,body {
  height: 100%;
  background-color: #edeef0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  font-weight: normal;
  font-style: normal;
  margin: 0;
  padding: 0;
}

.page-wrap {
  margin: 0 auto;
  margin-top: 20px;
  max-width: 550px;
  border: 1px solid #e3e4e8;
  border-radius: 4px;
  background-color: #fff;
  height: calc(100% - 90px);
}

.empty-msg {
  margin-top: 40px;
  font-size: 24px;
  color: #aaa;
  text-align: center;
}
</style>
