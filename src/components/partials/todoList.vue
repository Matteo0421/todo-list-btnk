<template>
    <div class="logo text-center mb-5">
      <img src="../../assets/img/BTINKEENG_esteso_positivo 1.jpg" alt="logo">
    </div>
  
    <div class="new-task">
      <input v-model.trim="newTask" @keyup.enter="addTask" placeholder="Nuovo task" type="text">
      <input v-model.trim="newDescription" placeholder="Descrizione" type="text">
      <button @click="addTask">Aggiungi</button>
      <p class="error">{{ errorMessage }}</p>
    </div>
  
    <div class="task-container">
      <ul v-if="taskList.length > 0">
        <li 
          v-for="(task, indice) in taskList" 
          :key="indice" 
          :class="{ done: task.done }" 
          @click="toggleDone(task)">
          <span>{{ task.text }}</span>
          <i @click.stop="rimuoviTask(indice)" class="fa-solid fa-trash-can"></i>
          <p v-if="task.description">{{ task.description }}</p> <!-- Mostra la descrizione -->
        </li>
      </ul>
      <h3 v-else>Non ci sono Task</h3>
    </div>
  </template>
  
  <script setup lang="ts">
  import { reactive, ref } from 'vue';
  
  interface Task {
    text: string;
    done: boolean;
    description: string; // Aggiunto il campo descrizione
  }
  
  const taskList = reactive<Task[]>([
    { text: 'fare la todolist', done: true, description: 'Compilare la lista delle cose da fare' },
    { text: 'studiare vue.js', done: true, description: 'Studiare i concetti base di Vue.js' },
    { text: 'ripetere css', done: false, description: 'Ripassare le regole CSS' },
    { text: 'giocare alla playstation', done: false, description: 'Giocare al nuovo videogioco' },
  ]);
  
  const newTask = ref<string>('');
  const newDescription = ref<string>(''); // Nuova ref per la descrizione
  const errorMessage = ref<string>('');
  
  function rimuoviTask(indice: number): void {
    if (taskList[indice].done) {
      taskList.splice(indice, 1);
    } else {
      errorMessage.value = 'ERRORE!!! la task deve essere eseguita per essere eliminata';
    }
  }
  
  function addTask(): void {
    errorMessage.value = '';
    if (newTask.value.length >= 5 && newDescription.value.length > 0) {
      taskList.unshift({ 
        text: newTask.value, 
        done: false, 
        description: newDescription.value // Aggiungi la descrizione
      });
      newTask.value = '';
      newDescription.value = ''; // Resetta anche il campo descrizione
      errorMessage.value = '';
    } else {
      errorMessage.value = 'ERRORE!!! il testo deve essere almeno di 5 caratteri e la descrizione non può essere vuota';
    }
  }
  
  function toggleDone(task: Task): void {
    task.done = !task.done;
  }
  </script>
  
  <style scoped>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  body {
    font-family: 'Lato', sans-serif;
  }
  
  img {
    max-width: 100%;
  }
  
  .new-task {
    text-align: center;
  }
  
  .new-task input {
    border-radius: 10px;
    padding: 10px 15px;
    border: 1px solid lightgray;
    margin: 5px;
    width: 300px;
  }
  
  .new-task button {
    border-radius: 10px;
    padding: 10px 15px;
    border-width: 1px;
    cursor: pointer;
  }
  
  .error {
    color: red;
    font-size: 0.9rem;
  }
  
  .task-container {
    background-color: #F5F7F7;
    border-radius: 10px;
    margin-top: 40px;
    padding: 30px;
  }
  
  .task-container ul {
    list-style: none;
  }
  
  .task-container li {
    line-height: 40px;
    border-bottom: 1px solid lightgray;
    padding: 0 15px;
    position: relative; /* Per gestire il posizionamento della trash can */
  }
  
  .task-container li:hover {
    background-color: #e0e0e0; /* Colore di sfondo quando si passa il mouse */
  }
  
  .task-container li i {
    float: right;
    line-height: 40px;
    cursor: pointer;
  }
  
  .task-container li i:hover {
    color: red;
  }
  
  .task-container li.done {
    text-decoration: line-through;
  }
  
  .task-container li p {
    font-size: 0.9rem;
    color: gray; /* Colore della descrizione */
  }
  </style>
  