<template>
  <div id="todo-list">
    <div v-for="[key, value] of todos" :key="key">
      <TodoListItem :title="value.title" :description="value.description" />
    </div>
  </div>
</template>

<script>
import TodoListItem from './TodoListItem'

export default {
  components: {
    TodoListItem,
  },
  props: {
    todos: {
      type: Map,
      required: true,
    },
  },
  created() {
    this.todos.forEach((value, key) => {
      console.log({ description: value.description, key })
    })
  },
}
</script>

<style>
#todo-list {
  display: flex;
  flex-direction: column;
  border-radius: 5px;
  box-shadow: 0 2px 5px #eee;
  padding: 20px;
}
</style>
