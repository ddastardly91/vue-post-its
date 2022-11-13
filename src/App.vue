<template>
   <main>
      <div v-if="showModal" @click.self="showModal = false" class="overlay">
         <div class="modal">
            <input
               v-model="newNote.title"
               type="text"
               placeholder="Enter a title..."
            />
            <textarea
               v-model="newNote.body"
               name="note"
               id="note"
               placeholder="Enter note text..."
            ></textarea>
            <span class="modal-error" v-if="newNoteError[1]">{{
               newNoteError[0]
            }}</span>
            <button @click="addNote">Add Note</button>
         </div>
      </div>
      <div class="container">
         <header>
            <h1>Notes</h1>
            <button @click="showModal = true" class="btn-add">+</button>
         </header>
         <div class="cards-container">
            <div class="card">
               <h3 class="card-title">This is a note</h3>
               <p class="card-body">
                  To create a note like this click on the add note button in the
                  top-right corner, you can then add a title and body text.
               </p>
               <p class="card-date">13/11/2022</p>
            </div>
            <div
               v-for="note in notes"
               :key="note.id"
               class="card"
               :style="{ backgroundColor: note.background }"
            >
               <h3 class="card-title">{{ note.title }}</h3>
               <p class="card-body">
                  {{ note.body }}
               </p>
               <p class="card-date">{{ note.date.toLocaleDateString() }}</p>
            </div>
         </div>
      </div>
   </main>
</template>

<script setup>
import { ref } from "vue";

const showModal = ref(false);
const newNoteError = ref(["Something went wrong.", false]);
const newNote = ref({ title: "", body: "" });
const notes = ref([]);

const addNote = () => {
   if (newNote.value.title == "") {
      newNoteError.value[0] = "You must enter a title.";
      newNoteError.value[1] = true;

      setTimeout(() => {
         newNoteError.value[1] = false;
      }, 4000);

      return false;
   }

   if (newNote.value.body == "") {
      newNoteError.value[0] = "You must enter some note text.";
      newNoteError.value[1] = true;

      setTimeout(() => {
         newNoteError.value[1] = false;
      }, 4000);

      return false;
   }

   if (newNote.value.title.length < 3) {
      newNoteError.value[0] = "Title must contain at least 3 characters.";
      newNoteError.value[1] = true;

      setTimeout(() => {
         newNoteError.value[1] = false;
      }, 4000);

      return false;
   }

   if (newNote.value.body.length < 8) {
      newNoteError.value[0] = "Body must contain at least 8 characters.";
      newNoteError.value[1] = true;

      setTimeout(() => {
         newNoteError.value[1] = false;
      }, 4000);

      return false;
   }

   notes.value.push({
      id: Math.random(),
      title: newNote.value.title,
      body: newNote.value.body,
      date: new Date(),
      background: getRandomColor(),
   });

   newNote.value = {};
   showModal.value = false;
};

const getRandomColor = () => {
   const color = "hsl(" + Math.random() * 360 + ", 75%, 75%)";
   return color;
};
</script>

<style scoped>
main {
   height: 100vh;
   width: 100vw;
}

.container {
   max-width: 1280px;
   margin: 0 auto;
   padding: 20px;
}

header {
   display: flex;
   justify-content: space-between;
   align-items: center;
}

h1 {
   font-weight: bold;
   margin-bottom: 25px;
   font-size: 75px;
}

.btn-add {
   display: flex;
   align-items: center;
   justify-content: center;
   border: none;
   padding: 15px;
   width: 50px;
   height: 50px;
   cursor: pointer;
   background-color: tomato;
   border-radius: 50%;
   font-size: 30px;
   color: inherit;
}

.cards-container {
   display: flex;
   flex-wrap: wrap;
   justify-content: center;
}

.card {
   width: 280px;
   height: 225px;
   background-color: teal;
   padding: 10px;
   margin: 10px;
   border-radius: 15px;
   color: white;

   display: flex;
   flex-direction: column;
   justify-content: space-between;
}

.card-title {
   font-weight: bold;
}

.card-date {
   font-size: 16px;
   font-style: italic;
   text-align: right;
}

.overlay {
   position: fixed;
   top: 0;
   width: 100vw;
   height: 100vh;
   background-color: rgba(0, 0, 0, 0.2);
   backdrop-filter: blur(5px);

   display: flex;
   align-items: center;
   justify-content: center;

   z-index: 10;
}

.modal {
   max-height: 70vh;
   position: relative;
   width: 650px;
   background-color: white;
   border-radius: 10px;
   padding: 20px;

   display: flex;
   flex-direction: column;
}

.modal input {
   outline: none;
   border: none;
   border-bottom: 1px solid lightgray;
   padding: 5px 0;
   margin-bottom: 20px;
   font-size: 28px;
   height: 45px;
   color: #333;
}
.modal textarea {
   min-width: 100%;
   min-height: 100px;
   max-width: 100%;
   outline: none;
   border: none;
   border-bottom: 1px solid lightgray;
   font-family: inherit;
   font-size: 20px;
   color: #333;
   margin-bottom: 20px;
}

.modal button {
   padding: 10px;
   background-color: teal;
   border: none;
   color: white;
   border-radius: 15px;
   font-weight: bold;
   font-size: 18px;
}

.modal-error {
   color: tomato;
   font-size: 16px;
   margin-bottom: 15px;
}

button {
   cursor: pointer;
}

/* Mobile Phones */
@media only screen and (max-width: 780px) {
   .card {
      width: 100%;
   }
}

@media only screen and (min-width: 780px) {
   .card {
      width: 350px;
   }
}
@media only screen and (min-width: 1150px) {
   .card {
      width: 20%;
   }
}
</style>
