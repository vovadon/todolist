<template>
  <div class="wrapper" v-bind:class="{'listIsEmpty':isListEmpty}">
    <form id="addTask" @submit="addTodo">
      <input type="time" id="appt" v-model="time">
      <div class="input-wrap">
        <input type="text" placeholder="Напишите задачу..." v-model="title" required>
        <button type="submit" form="addTask" >
          <i class="glyphicon glyphicon-plus w3-large"></i>
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import uuid from 'uuid';

export default {
  name: 'AddTodo',
  data() {
    return {
      title: '',
      time: ''
    }
  },
  props: {
    isListEmpty: Boolean,
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        id: uuid.v4(),
        title: this.title,
        time: this.time === '' ? 'Не указано' : this.time,
        completed: false
      }

      this.$emit('add-todo', newTodo);

      this.title = this.time = '';
    }
  }
}
</script>

<style scoped>
.wrapper {
  padding: 12px 12px;
  background-color: #fafbfc;
  border-radius: 4px 4px 0 0;
}

form {
  display: flex;
}

input[type=time] {
  border: 1px solid #d3d9de;
  border-radius: 4px;
  margin-right: 10px;
  width: 68px;
}

input[type=text] {
  font-size: 13px;
  border: none;
  margin: 7px 5px 8px 10px;
  width: 100%;
}

input[type=text]:focus {
  border-color: #5181b8;
}

input:required {
  box-shadow:none;
}

.input-wrap {
  background-color: #fff;
  border: 1px solid #d3d9de;
  border-radius: 4px;
  display: flex;
  flex: auto;
}

.input-wrap button {
  width: 32px;
  height: 36px;
  border: none;
  background: transparent;
}

.input-wrap i {
  cursor: pointer;
  color: #555;
}

.input-wrap i:hover {
  color: #444;
}

.listIsEmpty {
  border-radius: 4px;
}
</style>