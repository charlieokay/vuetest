<template>
  <h1>这个是todolist</h1>
  <TodoHeader></TodoHeader>
  <TodoBody></TodoBody>
  <TodoFooter></TodoFooter>
</template>

<script>
import TodoBody from "./todolist/TodoBody.vue";
import TodoFooter from "./todolist/TodoFooter.vue";
import TodoHeader from "./todolist/TodoHeader.vue";
export default {
  components: { TodoBody, TodoFooter, TodoHeader },
};
</script>

<style>
</style>