<template>
  <div id="app">
    <Header />
    <AddTodo v-bind:todos="todos" v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
import axios from "axios";
import krx from "krx-stock-api";

export default {
  name: "App",
  components: { Header, Todos, AddTodo },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    async addTodo(todo) {
      const { title, completed } = todo;
      const { data } = await axios.post(
        "https://jsonplaceholder.typicode.com/todos",
        {
          title,
          completed,
        }
      );
      this.todos = [...this.todos, data];
    },
  },
  async created() {
    // const res = await axios.get(
    //   "http://asp1.krx.co.kr/servlet/krx.asp.XMLSiseEng?code=005930"
    // );
    const res = await krx.getStock("005930");
    console.log(res);
    // this.todos = data;
  },
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

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
