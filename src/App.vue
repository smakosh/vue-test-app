<template>
  <div id="app">
    <form @submit.prevent="handleSubmit">
      <input name="name" v-model="name" />
      <button type="button" v-on:click="handleSubmit" form="name">
        Submit
      </button>
    </form>

    <form @submit.prevent="addTodo">
      <input name="title" v-model="title" />
      <button type="button" form="todos" v-on:click="addTodo">Add</button>
    </form>
    <ul v-if="todos.length > 0">
      <li v-for="todo in todos" :key="todo.id">
        <h4>{{ todo.title }}</h4>
        <button type="button" v-on:click="removeTodo(todo.id)">Delete</button>
      </li>
    </ul>
    <HelloWorld v-bind:msg="name" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  data: function () {
    return {
      name: "",
      title: "",
      todoId: 0,
      todos: [],
    };
  },
  methods: {
    handleName: function (event) {
      this.name = event.target.value;
    },
    handleSubmit: function (e) {
      e.preventDefault();
      alert(this.name);
    },
    addTodo: function (e) {
      e.preventDefault();
      this.todos.unshift({
        id: this.todoId++,
        title: this.title,
        completed: false,
      });
      this.title = "";
      this.todoId++;
    },
    removeTodo: function (id) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
  },
  components: {
    HelloWorld,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
