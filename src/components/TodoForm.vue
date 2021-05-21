<template>
  <div id="todo-form">
    <h2>Add New Note</h2>
    <input v-model="titleField" type="text" name="title" placeholder="Title" />
    <input v-model="descriptionField" type="text" name="description" placeholder="Description" />
    <button @click="handleSave">Save</button>
  </div>
</template>

<script>
export default {
  props: {
    onSave: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      titleField: '',
      descriptionField: '',
    };
  },
  methods: {
    handleSave() {
      this.onSave({
        title: this.titleField,
        description: this.descriptionField,
      });

      this.titleField = '';
      this.descriptionField = '';
    },
  },
};
</script>

<style>
#todo-form {
  display: grid;
  grid-template-columns: 1fr 1fr 200px;
  width: 100%;
  gap: 10px;
  padding: 10px;
  background: #eee;
}

#todo-form h2 {
  grid-column: 1 / -1;
  margin: 15px 0 2px;
}

#todo-form input {
  border: 0;
  width: 100%;
  height: 40px;
  background: #fff;
  font-size: 15px;
}
</style>
