<template>
  <div class="noteItem">
    <h3 style="margin-bottom: 0">{{ title }}</h3>
    <span>{{ content }}</span>
    <div style="display: flex; gap: 0.25em">
      <button @click="editNote">Edit</button>
      <button @click="deleteNote">Delete</button>
    </div>
  </div>
</template>
<script setup>
import { ref, reactive, defineProps, defineEmits } from "vue";

const props = defineProps(["title", "content"]);
const emit = defineEmits(["delete", "edit"]);

const deleteNote = () => {
  let response = confirm("Are you sure to delete this note?");
  response ? emit("delete", props.title) : null;
};

const editNote = () => {
  emit("edit", props.title);
};
</script>
<style scoped>
.noteItem {
  display: flex;
  padding: 0.125em;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;
  gap: 0.5em;
  border: 1px solid gray;
  width: 50%;
  border-radius: 0.25em;
}
</style>
