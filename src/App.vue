<script setup>
import {ref} from "vue";

const showModal = ref(false)
const errorMessage = ref("")
const newNote = ref("")
const notes = ref([]);

function getRandomColor() {
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)"
}

const addNotes = () => {
  if(newNote.value.length < 10) {
    return errorMessage.value= "Note needs to be 10 characters or more"
  }
  notes.value.push({
    id: Math.floor(Math.random() * 100000),
    text: newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor()  
  });

  showModal.value = false;
  newNote.value = ""
  errorMessage.value = ""
}


</script>



<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNotes">Add Note</button>
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
          v-for="note in notes"
          :key="note.id"
            class="cards" 
            :style="{backgroundColor: note.backgroundColor}
          ">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>

      </div>
    </div>
  </main>
</template>

<style scoped>
  main{
    background-color: white;
    width: 100vw;
    height: 100vh;
  }

  .container{
    max-width: 1000px; 
    padding: 10px;
    margin: 0 auto ;
  }

  header{
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  h1{
    font-weight: bold;
    font-size: 75px;
    margin-bottom: 25px;
  }

  header button{
    border: none;
    height: 50px;
    width: 50px;
    cursor: pointer;
    border-radius: 100%;
    color: white;
    background-color: rgba(21, 20, 20);
    font-size: 20px;
  }

  .cards{
    width:225px;
    height: 225px;
    background-color: rgb(237, 187, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;

  }

  .date{
    font-size: 12px;
    font-weight: bold;
  }

  .cards-container{
    display: flex;
    flex-wrap: wrap;
  }

  .overlay{
    width:100%;
    height: 100%;
    background-color: rgba(0,0,0,0.77);
    position: absolute;
    z-index: 10px; 
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal{
    width: 750px;
    background-color: white;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
    border-radius: 10px;
  }

  button{
    width: 100%;
    padding: 10px 20px;
    color: white;
    background-color: blueviolet;
    margin-top: 15px;
    cursor: pointer;
    font-size: 20px;
    border:none;
  }

  .modal .close{
    background-color: rgb(173, 17, 17);
  }

  .modal p {
    color: rgb(173, 17, 17);
    font-weight: bold;
  }
</style>