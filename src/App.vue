<template>
  <div id="app">
    <h1>TODO LIST</h1>

    <TodoForm :on-save="saveTodo" />

    <TodoList :todos="todos" :on-delete="deleteTodo" />
  </div>
</template>

<script>
import TodoList from './components/TodoList';
import TodoForm from './components/TodoForm';

export default {
  name: 'App',
  components: {
    TodoList,
    TodoForm,
  },
  data() {
    return {
      todos: new Map([
        [1, { title: 'Todo', description: 'Finalizar app de todos' }],
        [2, { title: 'Todo 2', description: 'Finalizar tarfaz de casa' }],
      ]),
    };
  },
  methods: {
    saveTodo({ title, description, key = Date.now() }) {
      this.todos.set(key, { title, description });
    },
    deleteTodo({ key }) {
      this.todos.delete(key);
    },
  },
};
</script>

<style>
html,
body {
  margin: 0;
}

a {
  color: initial;
  text-decoration: none;
}

* {
  box-sizing: border-box;
  font-family: 'Montserrat', sans-serif;
}

#app {
  display: flex;
  flex-direction: column;
  width: 100vw;
  max-width: 1120px;
  margin: 0 auto;
}

#app h1 {
  text-align: center;
  width: 100%;
}
</style>
