<template>
  <ul class="todo-main">
    <todo-item v-for="item in list" :item="item" :key="item.id"></todo-item>
  </ul>
</template>

<script>
import  item from "components/todo-item"
export default {
  "name": "todo-list",
  "props":{
    "list":Array
  },
  "components": {
    "todo-item":item
  }
}
</script>

<style scoped>
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}
</style>
