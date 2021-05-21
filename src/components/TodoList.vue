<template>
  <div id="todo-list">
    <div v-for="[key, { title, description }] of todos" :key="key">
      <TodoListItem :id="key" :title="title" :description="description" :on-delete="onDelete" />
    </div>
  </div>
</template>

<script>
import TodoListItem from './TodoListItem';

export default {
  components: {
    TodoListItem,
  },
  props: {
    todos: {
      type: Map,
      required: true,
    },
    onDelete: {
      type: Function,
      required: true,
    },
  },
};
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
