<script setup>
import { ref } from 'vue'

const newNote = ref("");
const errorMessage = ref("");
const notes = ref([]);

const addNote = () => {
  if (newNote.value.length < 10) {
    return errorMessage.value = "Text must be 10 characters or more";
  }
  notes.value.push({
    id: Math.floor(Math.random() * 20),
    text: newNote.value,
    date: new Date().toLocaleDateString('en-US')
  })
  newNote.value = "";
  errorMessage.value = ""
}

const deleteNote = (id) => {
  const index = notes.value.findIndex(item => item.id === id)
  if (index !== -1) {
    notes.value.splice(index, 1)
  }
}
</script>

<template>
  <main>
    <div class="container">
      <header>
        <h1>Notes</h1>
      </header>
      <div class="input">
        <input type="text" v-model.trim="newNote" placeholder="Enter a note">
        <button @click="addNote">+</button>
      </div>
      <p v-if="errorMessage" class="errorMessage">{{ errorMessage }}</p>
      <div class="card-container">
        <div class="card" v-for="note in notes" :key="note.id">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date }}</p>
          <p class="date">{{ note.id }}</p>
          <i class="fa-solid fa-trash delete" @click="deleteNote(note.id)"></i>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 100vh;
  width: 100vw;
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
}

h1 {
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 50px;
}

.input {
  width: 600px;
  height: 40px;
  margin: 0 auto 30px auto;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
  border: 1px solid black;
}

input {
  width: 90%;
  height: 90%;
  border-radius: 5px;
  border: none;
  outline: none;
  padding-left: 10px;
}

.input button {
  border: none;
  padding: 10px;
  width: 40px;
  height: 40px;
  background-color: rgb(21, 20, 20);
  /* border-radius: 100%; */
  color: white;
  font-size: 14px;
  cursor: pointer;
}


.card-container {
  width: 600px;
  height: 500px;
  box-shadow: 1px 1px 8px #eeeeee;
  border-radius: 20px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
}

.card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 60px;
  border-bottom: 1px solid rgb(228, 228, 228);
  margin: 0 30px;
}

.card p {
  font-size: 14px;
}

.errorMessage {
  color: red;
  text-align: center;
}

.delete {
  cursor: pointer;
}
</style>
