<template>
  <main>
    <div v-if="showModal" class="overleay">
      <div class="modal">
        <textarea
          name="note"
          id="note"
          cols="30"
          rows="10"
          v-model.trim="newNote"
        ></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
        <button @click="showModal = false" class="close">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div
          class="card"
          v-for="note in notes"
          :key="note.id"
          :style="{
            backgroundColor: note.backgroundColor,
          }"
        >
          <p class="main-text">
            {{ note.text }}
          </p>
          <p class="date">{{ note.date.toLocaleDateString('en-US') }}</p>
        </div>
      </div>
    </div>
  </main>
</template>
<script setup>
import { ref } from 'vue';
const showModal = ref(false);
const newNote = ref('');
const notes = ref([]);
const errorMessage = ref('');

function getRandomColor() {
  return 'hsl(' + Math.random() * 360 + ', 100%, 75%)';
}

const addNote = () => {
  if (newNote.value.length < 10) {
    return (errorMessage.value = 'Note must be at least 10 characters');
  } else {
    notes.value.push({
      id: Math.floor(Math.random() * 1000000),
      text: newNote.value,
      date: new Date(),
      backgroundColor: getRandomColor(),
    });

    showModal.value = false;
    newNote.value = '';
    errorMessage.value = '';
  }
};
</script>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
  /* display: flex;
  justify-content: center;
  align-items: center; */
}
.container {
  max-width: 1000px;
  padding: 10px;
  margin: 0 auto;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
h1 {
  font-size: 75px;
  font-weight: bold;
  margin-bottom: 25px;
}
button header {
  border: none;
  padding: 10px;
  border-radius: 100%;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21, 20, 20);
  color: white;
  font-size: 20px;
}
.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}
.date {
  font-size: 12.5px;
  font-weight: bold;
}
.cards-container {
  display: flex;
  flex-wrap: wrap;
}
.overleay {
  position: absolute;

  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.775);
  z-index: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}
.modal {
  width: 750px;

  background-color: white;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  flex-direction: column;
}
.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background-color: blueviolet;
  border: none;
  color: white;
  margin-top: 15px;
}
.modal .close {
  background-color: red;
  color: white;
}
.modal p {
  color: red;
}
</style>
