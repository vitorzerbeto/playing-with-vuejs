<template>
  <div class="note-item">
    <h3>{{ title }}</h3>
    <p>{{ description }}</p>
    <button class="delete" @click="handleDelete">Delete</button>
    <button class="edit" @click="handleEdit">Edit</button>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: Number,
      required: true,
    },
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
      required: true,
    },
    onEdit: {
      type: Function,
      required: true,
    },
  },
  methods: {
    handleDelete() {
      this.onDelete({ key: this.id });
    },
    handleEdit() {
      this.onEdit({ key: this.id });
    },
  },
};
</script>

<style>
.note-item {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 2fr auto auto;
  padding: 10px 0;
  gap: 10px;
  border-bottom: 1px solid #eee;
}

.note-item h3,
.note-item p {
  margin: 0;
}
</style>
