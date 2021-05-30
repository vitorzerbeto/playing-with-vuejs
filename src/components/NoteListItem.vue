<template>
  <div class="note-item">
    <div class="content">
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
    <p class="created-at">{{ createdAt }}</p>
    <div class="actions">
      <button class="delete" @click="handleDelete">Delete</button>
      <button class="edit" @click="handleEdit">Edit</button>
    </div>
  </div>
</template>

<script>
import format from 'date-fns/format';
import differenceInSeconds from 'date-fns/differenceInSeconds';
import differenceInMinutes from 'date-fns/differenceInMinutes';
import differenceInHours from 'date-fns/differenceInHours';

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
  computed: {
    createdAt() {
      const now = Date.now();
      const diffInSeconds = differenceInSeconds(now, this.id);
      const diffInMinutes = differenceInMinutes(now, this.id);
      const diffInHours = differenceInHours(now, this.id);

      if (diffInSeconds < 60) {
        return `${diffInSeconds} seconds ago`;
      }

      if (diffInMinutes < 60) {
        return `${diffInMinutes} minutes ago`;
      }

      if (diffInHours < 24) {
        return `${diffInMinutes} hours ago`;
      }

      return format(this.id, 'MM/dd/yyyy');
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
  display: flex;
  flex-direction: column;
  height: 100%;
  min-height: 200px;
  padding: 10px;
  border: 1px solid #eee;
}

.note-item h3,
.note-item p {
  margin: 0;
}

.note-item .content {
  height: 100%;
}

.note-item .created-at {
  font-size: 12px;
  font-style: italic;
}
</style>
