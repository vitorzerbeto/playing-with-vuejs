<template>
  <div id="note-form">
    <h2>{{ formTitle }}</h2>
    <input v-model="title" :readonly="isEditing" type="text" name="title" placeholder="Title" />
    <div class="tabs">
      <div class="tab-headers">
        <button :class="{ active: tab === 'write' }" @click="changeTab('write')">White</button>
        <button :class="{ active: tab === 'preview' }" @click="changeTab('preview')">
          Preview
        </button>
      </div>
      <div :class="tabWriteClasses">
        <textarea v-model="description" name="description" placeholder="Description"></textarea>
      </div>
      <div :class="tabPreviewClasses">
        <Markdown :input="description" />
      </div>
    </div>
    <button :disabled="!canSave" @click="handleSave">Save</button>
    <button @click="handleClear">Cancel</button>
  </div>
</template>

<script>
import Markdown from './Markdown';

export default {
  components: {
    Markdown,
  },
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
      tab: 'write',
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
    tabWriteClasses() {
      return {
        write: true,
        tab: true,
        'tab--active': this.tab === 'write',
      };
    },
    tabPreviewClasses() {
      return {
        write: true,
        tab: true,
        'tab--active': this.tab === 'preview',
      };
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
    changeTab(tab) {
      this.tab = tab;
    },
  },
};
</script>

<style>
#note-form {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto auto 1fr auto;
  width: 100%;
  height: 100%;
  gap: 10px;
  padding: 10px;
  background: #eee;
}

#note-form h2 {
  grid-column: 1 / -1;
  margin: 15px 0 2px;
}

#note-form input {
  grid-column: 1 / -1;
  border: 0;
  width: 100%;
  height: 40px;
  background: #fff;
  font-size: 15px;
}

#note-form textarea {
  border: 0;
  width: 100%;
  background: #fff;
  font-size: 15px;
  resize: none;
  height: 100%;
  border-radius: 4px;
  border: 1px solid #999;
  background: #f8f8f8;
  padding: 5px;
}

#note-form textarea:focus {
  background: #fff;
}

#note-form button {
  height: 40px;
}

#note-form .tabs {
  display: grid;
  grid-template-rows: auto 1fr;
  grid-column: 1 / -1;
  height: 100%;
}

#note-form .tabs .tab-headers {
  width: 100%;
  display: flex;
}

#note-form .tabs .tab-headers button {
  display: block;
  border-radius: 4px 4px 0px 0px;
  border: 0;
  padding: 0 10px;
}

#note-form .tabs .tab-headers button.active {
  border-top: 1px solid #999;
  border-left: 1px solid #999;
  border-right: 1px solid #999;
  background: #fff;
}

#note-form .tab {
  display: flex;
  flex-direction: column;
  grid-column: 1 / -1;
  height: 100%;
  display: none;
  background: #fff;
  padding: 15px;
  border-bottom: 1px solid #999;
  border-left: 1px solid #999;
  border-right: 1px solid #999;
}

#note-form .tab.tab--active {
  display: block;
}
</style>
