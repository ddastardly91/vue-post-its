<template>
   <main>
      <div
         v-if="showModal"
         @click.self="showModal = !showModal"
         class="overlay"
      >
         <div class="modal">
            <input type="text" placeholder="Enter a title..." />
            <textarea
               name="note"
               id="note"
               placeholder="Enter note text..."
            ></textarea>
            <button>Add Note</button>
         </div>
      </div>
      <div class="container">
         <header>
            <h1>Notes</h1>
            <button @click="showModal = !showModal" class="btn-add">+</button>
         </header>
         <div class="cards-container">
            <div class="card">
               <h3 class="card-title">Lorem</h3>
               <p class="card-body">
                  Lorem ipsum dolor sit, amet consectetur adipisicing elit.
                  Soluta nesciunt nisi numquam officiis.
               </p>
               <p class="card-date">13/11/22</p>
            </div>
            <div class="card">
               <h3 class="card-title">Lorem</h3>
               <p class="card-body">
                  Lorem ipsum dolor sit, amet consectetur adipisicing elit.
                  Soluta nesciunt nisi numquam officiis.
               </p>
               <p class="card-date">13/11/22</p>
            </div>
         </div>
      </div>
   </main>
</template>

<script setup>
import { ref } from "vue";

const showModal = ref(false);
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
}

.card {
   width: 225px;
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

button {
   cursor: pointer;
}

/* Mobile Phones */
@media only screen and (max-width: 600px) {
   .card {
      width: 100%;
   }
}
</style>
