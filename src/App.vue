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
    <div class="container w-5/6 md:w-5/12 lg:w-4/12">
      <header>
        <h1>Notes</h1>
      </header>
      <div class="input">
        <input type="text" v-model.trim="newNote" placeholder="Enter a note">
        <button @click="addNote">+</button>
      </div>
      <p v-if="errorMessage" class="errorMessage">{{ errorMessage }}</p>
      <div class="card-container my-4">
        <div class="card py-2" v-for="note in notes" :key="note.id">
          <p class="main-text flex flex-wrap">{{ note.text }}</p>
          <p class="date mx-3">{{ note.date }}</p>
          <i class="fa-solid fa-trash delete mx-3" @click="deleteNote(note.id)"></i>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  font-family: 'Poppins', sans-serif;
  background-color: rgba(202, 202, 210, 0.276);
  height: 100vh;
  width: 100vw;
}

.container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: rgba(235, 201, 52, 0.976);
  padding: 20px 20px 30px 20px;
  border-radius: 10px;
  margin: auto;
  border: 2px solid black;
}

header {
  text-align: center;
}

header h1 {
  font-size: 50px;
}

.input {
  border: 1px solid black;
  height: 40px;
  margin: 0 auto;
  border-radius: 5px;
  display: flex;
  justify-content: space-between;
}

input {
  width: 95%;
  height: 100%;
  border-top-left-radius: 5px;
  border-bottom-left-radius: 5px;
  border: none;
  outline: none;
  padding-left: 10px;
  font-size: 14px;
}

.input button {
  border: none;
  width: 39px;
  height: 39px;
  background-color: rgb(21, 20, 20);
  color: white;
  font-size: 14px;
  font-weight: bold;
  cursor: pointer;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
}

.card-container {
  height: 350px;
  overflow: scroll;
}

.card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid rgb(38, 38, 38);
  border-radius: 3px;
  margin-right: 20px;
}

.card p {
  font-size: 13px;
}
.delete{
  cursor: pointer;
}

</style>
