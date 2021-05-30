<template>
  <div id="app">
    <h1>My Notes</h1>

    <NoteForm :note="noteToEdit" :on-save="saveNote" :on-clear="clearEditNote" />
    <NoteList :notes="notes" :on-delete="deleteNote" :on-edit="editNote" />
  </div>
</template>

<script>
import NoteList from './components/NoteList';
import NoteForm from './components/NoteForm';

export default {
  name: 'App',
  components: {
    NoteList,
    NoteForm,
  },
  data() {
    return {
      notes: new Map([
        [1, { title: 'Note', description: 'Finalizar app de notes' }],
        [2, { title: 'Note 2', description: 'Finalizar tarfaz de casa' }],
      ]),
      noteToEdit: undefined,
      isEditing: false,
    };
  },
  methods: {
    saveNote({ title, description, key }) {
      this.notes.set(key, { title, description });
    },
    deleteNote({ key }) {
      this.notes.delete(key);
    },
    editNote({ key }) {
      const { title, description } = this.notes.get(key);

      this.noteToEdit = { title, description, key };
      this.isEditing = true;
    },
    clearEditNote() {
      this.noteToEdit = undefined;
      this.isEditing = false;
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
