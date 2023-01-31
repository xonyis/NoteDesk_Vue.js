<script setup>
import {ref} from "vue";

  const showModal = ref(false);
  const newNotes = ref("");
  const errorMsg = ref("")
  const notes = ref([]);

  function getRandomColor() {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
    
  }

  const addNote = () => {
    if (newNotes.value.length < 5) {
      return errorMsg.value = "Note need to be 5 characters or more"
    }
    notes.value.push({
      id: Math.floor(Math.random() * 3000),
      text: newNotes.value,
      date: new Date(),
      bgcolor: getRandomColor(),
    });
    showModal.value = false;
    newNotes.value = "";
    errorMsg.value = "";

  }
</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <div><button class="close" @click="showModal = false">Close</button>
        <p v-if="errorMsg">{{ errorMsg }}</p></div>
        <textarea v-model.trim="newNotes" name="note" id="note" cols="30" rows="10"></textarea>
        <button @click="addNote">Add Notes</button>

      </div>
    </div>
    <div class="container">
      <header>
        <h1>Note Desk</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="card-container">
        <div v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor: note.bgcolor} ">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("fr-FR")}}</p>
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
    width: 82%;
    padding: 10px;
    margin: auto;
  }

  header {
    display: flex;
    justify-content: space-around;
    align-items: center;
  }

  .card-container {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
  }

  h1 {
    font-weight: bold;
    font-size: 50px;
    margin-bottom: 25px;
  }
  header button {
    width: 50px;
    height: 50px;
    padding: 10px;
    cursor: pointer;
    border: none;
    border-radius: 50px;
    font-size: 20px;
    transition:1s ease;
  }
  header button:hover {
    width: 65px;
    height: 65px;
    font-size: 25px;
  }
  .date {
    font-weight: bold;
    bottom: 0px;
  }

  .card {
    width: 250px;
    height: 300px;
    background: orange;
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-left: 20px;
    margin-right: 20px;
    color: #181818;
    margin-bottom: 2em;
  }

  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.707);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal {
  width: 60%;
  background: #fff;
  border-radius: 10px;
  padding: 30px;
  position: relative;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  flex-direction: column;
}

.modal textarea {
  width: 100%;
}

.modal .close {
  background-color: rgba(209, 31, 31, 0.888);
  margin-top: 10px;
  
}
.modal button {
  padding: 10px 20px;
  font-size: 20px;
  width: 100%;
  background: blueviolet;
  border: none;
  color: white;
  cursor: pointer;
  margin-top: 15px;
}

.modal p {
  color: red;
}
</style>