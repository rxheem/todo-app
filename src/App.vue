<template>
  <div id="app">
   <Todos v-bind:todos="todos"/>
  </div>
</template>

<script>

import Todos from './components/Todos';

export default {
  name: 'app',
  components: {
    Todos
  }, 
  data(){
    return {
      todos: [
        {
          id: 1, 
          title: 'Wash the dishes', 
          completed: false
        },
        {
          id: 2, 
          title: 'Take out the garbage', 
          completed: true
        },
        {
          id: 1, 
          title: 'Meeting with the boss', 
          completed: false
        },
        {
          id: 1, 
          title: 'Go to work', 
          completed: false
        }
      ]
    }
  }
}
</script>

<style scoped>
  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body{
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>
