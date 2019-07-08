<template>
  <div class="todo-item" >
    <div>
      <div class="chechbox-continer">
        <label class="wrap-chechbox">
          <input type="checkbox" v-on:change="markComplete">
          <span class="checkmark"></span>
        </label>
      </div>
      <div class="wrap-todo">
        <p><b>Время:</b> {{todo.time}}</p>
        <p v-bind:class="{'is-complete':todo.completed}">{{todo.title}}</p>
      </div>
    </div>
    <button @click="$emit('del-todo', todo.id)" class="del">
      <i class="material-icons w3-large">close</i>
    </button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
}
</script>

<style scoped>
.wrap-todo {
  display: inline-block;
}

.wrap-todo p {
}

.todo-item {
  display: -moz-box;
  display: -webkit-box;
}

.todo-item:hover i {
  visibility: visible;
}

.todo-item > div {
  display: -moz-box;
  display: -webkit-box;
  border-top: 1px solid #e7e8ec;
  flex: auto;
  padding: 12px;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: transparent;
  color: #aaa;
  border: none;
  border-top: 1px solid #e7e8ec;
  cursor: pointer;
  padding: 0;
}

.del i {
  padding: 12px 4px 0px 0;
  visibility: hidden;
}

.del i:hover {
  color: #666;
}

p {
  margin: 0;
}

input[type=checkbox] {
  margin: 0;
}

.chechbox-continer {
  position: relative;
  width: 30px;
}

.wrap-chechbox input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
}

.checkmark {
  position: absolute;
  top: 7px;
  left: 0;
  height: 24px;
  width: 24px;
  border: 1px solid #555;
  border-radius: 4px;
}

.wrap-chechbox:hover input ~ .checkmark {
  background-color: #ccc;
}

.wrap-chechbox input:checked ~ .checkmark {
  background-color: #555;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.wrap-chechbox input:checked ~ .checkmark:after {
  display: block;
}

.wrap-chechbox .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>