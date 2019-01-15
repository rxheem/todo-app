<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
/* Script imports */
import Todos from "./components/Todos";
import Header from "./components/layout/Header";
import AddTodo from "./components/AddTodo";
import uuid from "uuid";
import axios from "axios";

export default {
  name: "app",
  components: {
    Header,
    Todos,
    AddTodo
  },
  data() {
    return {
      // Right here we're initializing a blank array because the data will be fetched from an API
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`).then(
        res =>
          (this.todos = this.todos
            .filter(
              // Right here, we copy all the existing objects if their ID is no the ID passed.
              todo => todo.id !== id
            )
            .catch(err => console.log(err)))
      );
    },

    // Method to add a new Todo item to the object.
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios
        // We're using axios here to make a POST api request to the URl. It will return a JSON file with a list of TODOS
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })

        // We will join the existing todos we have here to the new todos
        .then(res => (this.todos = [...this.todos, res.data]))

        // Then we catch and log any errors just in case
        .catch(err => console.log(err));
    }
  },
  // Right here, the method will run automatically when the file is being executed. It is similar to an onLoad() method
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=50") // Fetches them, applying a limit fo 50

      // Then we set the todos to the the data held in the response from the server
      .then(res => (this.todos = res.data))

      // And we consoe.log() and error that we get
      .catch(err => console.log(err));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
