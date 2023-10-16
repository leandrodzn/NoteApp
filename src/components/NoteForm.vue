<template>
  <div>
    <h2>Add new note</h2>
    <input v-model="title" placeholder="Title" required />
    <textarea
      v-model="content"
      placeholder="Content"
      row="3"
      required
    ></textarea>
    <button @click="saveNote">Save note</button>
  </div>
</template>
<script setup>
import { ref, reactive, defineProps, defineEmits } from "vue";

const emit = defineEmits(["addNote"]);

let title = ref("");
let content = ref("");

const saveNote = () => {
  if (title.value.trim() != "" && content.value.trim() != "") {
    let note = {
      title: title.value.trim(),
      content: content.value.trim(),
    };
    emit("addNote", note);
    title.value = "";
    content.value = "";
  } else {
    alert("Write title and content");
  }
};
</script>
<style scoped>
div {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1em;
  width: 100%;
}
</style>
<style>
input,
textarea,
button {
  width: 50%;
}

button {
  background-color: #ff338e;
  color: white;
  padding: 0.5em;
  display: flex;
  align-items: center;
  justify-content: center;
}

button:hover {
  cursor: pointer;
}
</style>
