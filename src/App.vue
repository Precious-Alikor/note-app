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
    date: new Date().toLocaleDateString('en-US'),
    backgroundColor: randomColor(),
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

const randomColor = () => {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
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
      <p v-if="errorMessage" class="errorMessage mt-2">{{ errorMessage }}</p>
      <div class="card-container grid lg:grid-cols-4 gap-x-8 pb-10">
        <div class="card py-2" v-for="note in notes" :key="note.id">
          <div class="notes rounded p-4" :style="{ backgroundColor: note.backgroundColor }">
            <div class="flex justify-between">
              <p class="main-text flex flex-wrap break-all w-10/12">{{ note.text }}</p>
              <i class="fa-solid fa-trash delete" @click="deleteNote(note.id)"></i>
            </div>
            <p class="date mt-3">{{ note.date }}</p>

          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  font-family: 'Poppins', sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  width: 80%;
  height: 80vh;
}

header {
  text-align: center;
  margin-top: 20px;
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

.notes {
  margin-top: 30px;
  /* height: 180px; */
  color: black;
}

.card p {
  font-size: 13px;
}

.delete {
  cursor: pointer;
}
</style>
