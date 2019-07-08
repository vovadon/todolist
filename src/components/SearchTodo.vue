<template>
  <div class="header">
    <div class="main">
      <div class="wrapper" v-bind:class="{'onfocus':this.onfocus}">
        <div class="search-img">
          <i class="glyphicon glyphicon-search w3-large"></i>
        </div>
        <div class="search-wrap">
          <input type="text" placeholder="Начните вводить текст задачи..." v-model="query" @focus="searchFocusHandler" @blur="removeFocus" @input="changeHandler">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchTodo',
  data() {
    return {
      onfocus: false,
      query: ''
    }
  },
  methods: {
    searchFocusHandler() {
      this.onfocus = true;
    },
    removeFocus() {
      this.onfocus = false;
    },
    changeHandler() {
      this.$emit("change", this.query);
    }
  }
}
</script>

<style scoped>
.header {
  height: 70px;
  background-color: #333;
}

.wrapper {
  background-color: #555;
  display: flex;
  flex-direction: row;
  max-width: 638px;
  border-radius: 24px;
  height: 44px;
  margin: 0 auto;
}

.onfocus {
  background-color:#fff;
}

.search-wrap {
  flex: auto;
  display: flex;
  padding-right: 20px;
  padding-bottom: 1px;
}

.search-img {
  height: 44px;
  width: 44px;
}

.main {
  padding: 13px 0;
}

i {
  padding: 12px;
}

input {
  margin: 7px 0;
  height: 28px;
  width: 100%;
  background-color: transparent;
  border: none;
  color: rgba(0,0,0,.87);
  outline: none;
  font: 16px arial,sans-serif;
}

input::placeholder {
  color: #aaa;
}

input:focus::-moz-placeholder {
  color: transparent;
}
</style>