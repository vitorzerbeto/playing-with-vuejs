<template>
  <div id="note-form">
    <h2>{{ formTitle }}</h2>
    <input v-model="title" type="text" name="title" placeholder="Title" />
    <input v-model="description" type="text" name="description" placeholder="Description" />
    <button :disabled="!canSave" @click="handleSave">Save</button>
    <button :disabled="!isEditing" @click="handleClear">Cancel</button>
  </div>
</template>

<script>
export default {
  props: {
    onSave: {
      type: Function,
      required: true,
    },
    onClear: {
      type: Function,
      required: true,
    },
    note: {
      type: Object,
      default: undefined,
    },
  },
  data() {
    return {
      title: '',
      description: '',
      key: undefined,
      isEditing: false,
    };
  },
  computed: {
    canSave() {
      return (
        this.title !== '' &&
        this.title !== undefined &&
        this.description !== '' &&
        this.description !== undefined
      );
    },
    formTitle() {
      return this.title || 'Add New Note';
    },
  },
  watch: {
    note: function (note) {
      if (note) {
        this.title = note.title;
        this.description = note.description;
        this.key = note.key;
        this.isEditing = true;
      }
    },
  },
  methods: {
    handleClear() {
      this.title = '';
      this.description = '';
      this.key = undefined;
      this.isEditing = false;

      this.onClear();
    },
    handleSave() {
      this.onSave({
        key: this.key !== undefined ? this.key : Date.now(),
        title: this.title,
        description: this.description,
      });

      this.handleClear();
    },
  },
};
</script>

<style>
#note-form {
  display: grid;
  grid-template-columns: 1fr 1fr 200px 200px;
  width: 100%;
  gap: 10px;
  padding: 10px;
  background: #eee;
}

#note-form h2 {
  grid-column: 1 / -1;
  margin: 15px 0 2px;
}

#note-form input {
  border: 0;
  width: 100%;
  height: 40px;
  background: #fff;
  font-size: 15px;
}
</style>
