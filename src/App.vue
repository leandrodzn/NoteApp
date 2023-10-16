// ADA 3.1 Aplicación de notas - Integrantes: María Belen Couoh Chan & Leandro
Angel Dzib Nauat
<template>
  <div
    style="
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      width: 100%;
    "
  >
    <h1>Note App</h1>
    <NoteForm @addNote="addNote" />
    <NoteEditModal
      v-if="editMood"
      :note="noteInEdition"
      :index="indexNoteInEdition"
      @close="closeEditModal"
      @saveNote="saveEditedNote"
    />
    <NoteList :list="list" @deleteNote="deleteNote" @editNote="editNote" />
  </div>
</template>
<script setup>
import NoteForm from "./components/NoteForm.vue";
import NoteList from "./components/NoteList.vue";
import NoteEditModal from "./components/NoteEditModal.vue";
import { reactive, ref } from "vue";

let list = reactive([]);
let editMood = ref(false);
let noteInEdition = reactive({});
let indexNoteInEdition = ref(-1);

const addNote = (note) => {
  const exists = list.find((noteInList) => noteInList.title === note.title);
  !exists ? list.push(note) : alert("Note with that title exists yet");
};

const deleteNote = (title) => {
  const index = list.findIndex((note) => note.title === title);
  index != -1 ? list.splice(index, 1) : null;
};

// response when user clicks button edit in a note opening edition modal
const editNote = (title) => {
  const index = list.findIndex((note) => note.title === title);
  if (index != -1) {
    indexNoteInEdition.value = index;
    noteInEdition = list[index];
    editMood.value = true;
  }
};

const closeEditModal = () => {
  editMood.value = false;
  noteInEdition = {};
  indexNoteInEdition.value = -1;
};

const saveEditedNote = (note, index) => {
  // find the index in list when title is same that the title edited
  const indexSameName = list.findIndex(
    (noteInList) => noteInList.title === note.title
  );
  // if the title isn't in use or title belongs to the same note
  if (indexSameName === -1 || indexSameName == index) {
    list[index] = note;
    closeEditModal();
  } else {
    alert("Note with that title exists yet");
  }
};
</script>

<style>
body {
  min-height: 100vh;
  transition: color 0.5s, background-color 0.5s;
  line-height: 1.6;
  font-family: Inter, -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue",
    sans-serif;
  font-size: 15px;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
