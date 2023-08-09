<script setup>
import {ref} from 'vue'

const showModal = ref(false)
const newNote = ref("")
const notes = ref([])

function getRandomColor() {
  const color = "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  return color;
}

const noteTaken = ()=> {
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    color: getRandomColor(),
    date: new Date()
  }); 
  showModal.value = false;
  newNote.value = ""
}


</script>



<template>
  <main class="container">


    <div class="header">
      <h1>Notes 📝 ...</h1>
      <button @click=" showModal = true" >+</button>
    </div>
    <hr>
    <div  class="cards-container">
      <div v-for="note in notes"  class="cards" :style="{backgroundColor: note.color}">
        <div class="note-title">
          <p>{{ note.text }}</p>
        </div>

        <div class="note-date">
          <h6>{{note.date.toLocaleDateString("en-US")}}</h6>
        </div>

      </div>
    </div>

    <div v-if="showModal"  class="note-taking">
      <div class="input-container">
        <textarea v-model="newNote"  cols="30" rows="10">{{ newNote  }}</textarea>
        <div class="buttons-row">
          <button @click="noteTaken" class="btn-add">Add</button>
          <button @click="showModal=false"  class="btn-discard" >Discard</button>
        </div>
      </div>
    </div>

  </main>
</template>

<style scoped>

main {
  align-items: center;
  justify-content: center;
}

.container {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  height: 100vh;
}

.header {
  display: flex;
  flex-direction: row;
  width: 1000px;
  height: 100px;
  align-items: center;
  justify-content: space-between;
}

.header h1 {
  font-weight: bold;
  color: rgb(239, 239, 239);
}

.header button {
  font-size: 2em;
  background-color: rgb(88, 176, 131);
  border-radius: 8px;
  color: aliceblue;
  cursor: pointer;
  transition: ease-in-out;
  transition-duration: .5s;
  transition-delay: .1s;
}

.header button:hover{
  background-color: rgb(88, 176, 131);
  border-radius: 100px;
  transition-duration: .5s;
  transition-delay: .3s;
}

hr {
  width: 1000px;
  opacity: 20%;
  margin: 10px;
}

.cards-container {
  padding: 20px;
  margin: 20px;
  display: flex;
  flex-wrap: wrap;
  width: 1000px;
  height: fit-content;
  background-color: rgb(27, 27, 27);
}

.cards {
  margin: 20px;
  padding: 15px;
  background-color: rgb(251, 191, 62);
  height: fit-content;
  width: 200px;
  border-radius: 25px;
  color: rgb(18, 18, 18);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: start;
}

.note-title h4 {
  font-weight: bold;
  text-align: center;
}

.note-date h6 {
  justify-content: end;
  width: 200px;
  font-weight: bold;
  margin: 5px;
}

.note-taking {
  background-color: rgb(36, 36, 36);
  z-index: 100;
  display: flex;
  flex-direction: column;
  width: 700px;
  height: 500px;
  border-radius: 25px;
  align-items: center;
  justify-content: center;
  position: fixed;
  bottom: 100px;
}


.input-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: fit-content;
  height: fit-content;
  padding: 50px;
}

.input-container textarea {
  margin: 50px;
  padding: 50px;
  height: 300px;
  width: 500px;
  border-radius: 25px;
  background-color: rgb(236, 237, 225);
}
.buttons-row {
  display: flex;
  flex-direction: row;
}

.btn-add {
  width: 80px;
  padding: 10px;
  border-radius: 25px;
  background-color: rgb(88, 176, 131);
  margin: 10px;
  cursor: pointer;
  transition: cubic-bezier(0.25, 0.46, 0.45, 0.94);
  transition-duration: .3s;
  transition-delay: .1s;
}

.btn-add:hover{
  width: 120px;
  background-color: rgb(88, 176, 131);
  color: aliceblue;
  font-weight: bold;
}

.btn-discard {
  width: 80px;
  padding: 10px;
  border-radius: 25px;
  background-color: rgb(239, 148, 118);
  margin: 10px;
  cursor: pointer;
  transition: cubic-bezier(0.25, 0.46, 0.45, 0.94);
  transition-duration: .3s;
  transition-delay: .1s;
}

.btn-discard:hover{
  width: 120px;
  background-color: rgb(251, 175, 150);
  color: aliceblue;
  font-weight: bold;
}

</style>