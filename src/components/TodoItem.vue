<template>
  <div class="todo-item" v-bind:class="{'is-completed':todo.completed}">
    <p>
      <input type="checkbox" v-on:change="markComplete" />
      {{todo.title}}
      <button @click="$emit('del-todo', todo.id)" class="del">X</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1px dotted #ccc;
}
.is-completed {
  text-decoration: line-through;
}
</style>