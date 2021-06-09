<template>
  <div id="my-app">
    <div class="container">
      <h1>My Notes</h1>

      <NoteList :notes="notes" :on-delete="deleteNote" :on-edit="editNote" />

      <button title="Add Note" class="add-note" @click="openModal">+</button>
    </div>

    <Modal :is-active="isModalOpen" :on-close="clearEditNote">
      <NoteForm :note="noteToEdit" :on-save="saveNote" :on-clear="clearEditNote" />
    </Modal>
  </div>
</template>

<script>
import NoteList from './components/NoteList';
import NoteForm from './components/NoteForm';
import Modal from './components/Modal';

export default {
  name: 'App',
  components: {
    NoteList,
    NoteForm,
    Modal,
  },
  data() {
    return {
      notes: new Map(),
      noteToEdit: undefined,
      isEditing: false,
      isModalOpen: false,
    };
  },
  mounted() {
    const localStorageNotes = localStorage.getItem('notes');

    if (localStorageNotes) {
      try {
        const objFromLocalStorage = JSON.parse(localStorageNotes);
        const entries = Object.entries(objFromLocalStorage).map((note) => {
          const [key, value] = note;

          return [parseInt(key), value];
        });

        this.notes = new Map(entries);
      } catch (e) {
        console.log(e);
        localStorage.removeItem('notes');
      }
    }
  },
  methods: {
    persistNotes() {
      const mapToObj = Object.fromEntries(this.notes);
      const json = JSON.stringify(mapToObj);

      localStorage.setItem('notes', json);
    },
    saveNote({ title, description, key }) {
      this.notes.set(key, { title, description });

      this.persistNotes();
      this.closeModal();
    },
    deleteNote({ key }) {
      this.notes.delete(key);

      this.persistNotes();
    },
    editNote({ key }) {
      const { title, description } = this.notes.get(key);

      this.noteToEdit = { title, description, key };
      this.isEditing = true;

      this.openModal();
    },
    clearEditNote() {
      this.noteToEdit = undefined;
      this.isEditing = false;

      this.closeModal();
    },
    openModal() {
      this.isModalOpen = true;
    },
    closeModal() {
      this.isModalOpen = false;
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

.container {
  width: 100%;
  display: flex;
  flex-direction: column;
}

#my-app {
  width: 100vw;
  max-width: 1120px;
  margin: 0 auto;
}

#my-app h1 {
  text-align: center;
  width: 100%;
}

#my-app .add-note {
  display: flex;
  position: fixed;
  bottom: 1vw;
  right: calc((100vw - 1120px) / 2);
  width: 60px;
  height: 60px;
  border-radius: 50%;
  background: purple;
  border: none;
  cursor: pointer;
  color: #fff;
  font-size: 55px;
  padding: 0;
  align-items: center;
  justify-content: center;
  font-weight: 200;

  transition: transform 0.2s ease;
}
#my-app .add-note:hover {
  transform: scale(1.1);
}
#my-app .add-note:active {
  transform: scale(1.05);
}
</style>
