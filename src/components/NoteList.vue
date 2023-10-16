<template>
  <div>
    <h2>Notes List</h2>
    <span v-if="list.length === 0">List empty</span>
    <NoteItem
      v-else
      v-for="(note, index) in list"
      :key="index"
      :title="note.title"
      :content="note.content"
      @delete="deleteNote"
      @edit="editNote"
    ></NoteItem>
  </div>
</template>
<script setup>
import { ref, reactive, defineProps, defineEmits } from "vue";
import NoteItem from "./NoteItem.vue";

defineProps(["list"]);
const emit = defineEmits(["deleteNote", "editNote"]);

const deleteNote = (title) => {
  emit("deleteNote", title);
};

const editNote = (title) => {
  emit("editNote", title);
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
