<script setup>
import { ref } from 'vue';

const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);
const errorMessage = ref("");

function getRandomColor(){
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote = () =>{
  if(newNote.value.length < 10){
   
    return errorMessage.value = "Your Input is less than 10 Characters"
  }
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor(),
  });
  showModal.value = false;
  newNote.value = "";
  errorMessage.value = "";
}
</script>


<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <button @click="showModal = false" class="closeNote">X</button>
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button class="add" @click="addNote">ADD NOTE</button>
      
      </div>
    </div>

    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
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
  margin: 0 auto;
  padding: 20px;
  box-sizing: border-box;
  width: 1000px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header h1 {
  font-family: sans-serif;
  font-size: 40px;
  font-weight: bold;
  color: rgba(1, 0, 48, 0.911);
}

header button {
  font-size: 30px;
  height: 50px;
  width: 50px;
  border: none;
  border-radius: 50px;
  background-color: rgb(53, 28, 58);
  color: white;
  cursor: pointer;
}

.card {
  width: 170px;
  height: 170px;
  background-color: rgba(2, 119, 214, 0.856);
  padding: 10px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
  font-size: 15px;
}

.date {
  font-size: 11.5px;
  font-weight: bold;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(16, 0, 53, 0.616);
  z-index: 10;
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

.modal .add{
  padding: 10px 15px;
  font-size: 20px;
  margin-top: 8px;
  cursor: pointer;
  background-color: rgba(27, 13, 41, 0.938);
  color: white;
  border-radius: 18px;
  border: 0;
}

.modal .add:hover{
  background-color: rgb(49, 5, 94);
}

.modal .closeNote{
  width: 40px;
  height: 40px;
  font-weight: bold;
  display: flex-direction;
  float: right;
}

.modal p{
  color: red;
  font-size: 13px;
}
</style>
