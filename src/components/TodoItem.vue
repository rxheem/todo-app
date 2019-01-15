<template>
  <div class="todo-item" v-bind:class="{'is-complete': todo.completed}">
    <input type="checkbox" v-on:change="markComplete">
    <p>{{todo.title}}</p>
    <button @click="$emit ('del-todo', todo.id)" class="del">x</button>
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
};
</script>

<style scoped>
* {
  display: flow-root;
}

.todo-item {
  background-color: #f4f4f4;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}

.is-complete {
  text-decoration: line-through;
}

.del {
  background: #ff3333;
  float: right;
  bottom: 50%;
  top: 50%;
}
</style>
