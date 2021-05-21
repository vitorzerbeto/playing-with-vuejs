<template>
  <div class="todo-item">
    <h3>{{ title }}</h3>
    <p>{{ description }}</p>
    <button class="delete">Delete</button>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      required: true,
    },
    onDelete: {
      type: Function,
      default: () => {},
    },
  },
}
</script>

<style>
.todo-item {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 2fr 100px;
  padding: 10px 0;
  gap: 10px;
  border-bottom: 1px solid #eee;
}

.todo-item h3,
.todo-item p {
  margin: 0;
}
</style>
