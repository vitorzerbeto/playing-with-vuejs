<template>
  <div id="note-list">
    <div v-for="[key, { title, description }] of notes" :key="key">
      <NoteListItem
        :id="key"
        :title="title"
        :description="description"
        :on-delete="onDelete"
        :on-edit="onEdit"
      />
    </div>
  </div>
</template>

<script>
import NoteListItem from './NoteListItem';

export default {
  components: {
    NoteListItem,
  },
  props: {
    notes: {
      type: Map,
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
};
</script>

<style>
#note-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
  margin-top: 10px;
}
</style>
