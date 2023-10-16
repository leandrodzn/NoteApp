<template>
  <div id="modal" class="modal">
    <div class="modal-content">
      <span class="close" @click="close">&times;</span>
      <div class="form">
        <h2>Edit note</h2>
        <input v-model="title" placeholder="Title" required />
        <textarea
          v-model="content"
          placeholder="Content"
          row="3"
          required
          style="margin-top: 10px"
        ></textarea>
        <button style="margin-top: 10px" @click="saveNote">Save note</button>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, reactive, defineProps, defineEmits } from "vue";

const emit = defineEmits(["saveNote", "close"]);
const props = defineProps(["note", "index"]);

let title = ref(props.note.title);
let content = ref(props.note.content);

const close = () => {
  emit("close");
};

const saveNote = () => {
  if (title.value.trim() != "" && content.value.trim() != "") {
    let note = {
      title: title.value.trim(),
      content: content.value.trim(),
    };
    emit("saveNote", note, props.index);
  } else {
    alert("Write title and content");
  }
};
</script>
<style scoped>
.modal {
  display: block;
  position: fixed; /* Posición fija */
  z-index: 1; /* Se situará por encima de otros elementos de la página*/
  padding-top: 200px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto; /* Se activará el scroll si es necesario */
  background-color: rgba(0, 0, 0, 0.5); /* Color negro con opacidad del 50% */
}

.modal-content {
  position: relative; /* Relativo con respecto al contenedor -modal- */
  background-color: white;
  margin: auto; /* Centrada */
  padding: 20px;
  width: 60%;
  -webkit-animation-name: animarsuperior;
  -webkit-animation-duration: 0.5s;
  animation-name: animarsuperior;
  animation-duration: 0.5s;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

/* Add Animation */
@keyframes animatetop {
  from {
    top: -300px;
    opacity: 0;
  }
  to {
    top: 0;
    opacity: 1;
  }
}

@keyframes animarsuperior {
  from {
    top: -300px;
    opacity: 0;
  }
  to {
    top: 0;
    opacity: 1;
  }
}

.close {
  color: black;
  float: right;
  font-size: 30px;
  font-weight: bold;
  user-select: none;
}

.close:hover,
.close:focus {
  color: #000;
  text-decoration: none;
  cursor: pointer;
}
</style>
<style>
#modal input,
#modal textarea,
#modal button {
  width: 100%;
}
</style>
