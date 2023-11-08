<script setup>
import { ref } from 'vue';

let newTask = ref('')

let taskList = ref([
  {
    name: 'Estudiar',
    done: true
  },
  {
    name: 'Comer',
    done: false
  },
  {
    name: 'Dormir',
    done: false
  }
])

function setDone(index) {
  taskList.value[index].done = true
}

function addTask() {
  if(newTask.value.trim() === '') return
  taskList.value.push({
    name: newTask.value,
    done: false
  })
  newTask.value = ''
}
</script>

<template>
  <div class="container">
    <h1>Lista de Tareas</h1>
    <p class="subtitle">{{ newTask }}</p>

    <div>
      <div class="task" :class="{done: task.done}" v-for="(task, index) in taskList" :key="index">{{ task.name }} <span @click="setDone(index)" class="button">X</span></div>
      <!-- <div class="task">Tarea2 <span class="button">X</span></div> -->
    </div>

    <input v-model="newTask" @keypress.enter="addTask" type="text" placeholder="Escriba su tarea">
    <p v-show="newTask != ''" class="help">Presiona enter para agregar la tarea</p>
  </div>
 
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
.help{
  font-size: 8px;
  opacity: 0.6;
  margin: 0;
}
.button{
  background-color: #A52502;
  display: inline-block;
  padding: 0 6px;
  border-radius: 3px;
}

.button:hover{
  cursor: pointer;
}

input{
  margin-top: 12px;
  border: none;
  border-radius: 3px;
  padding: 2px 6px;
  outline: none;
  /* width: calc(100% - 12px); */
  width: 100%;
  box-sizing: border-box;
}

input::placeholder{
  opacity: 0.4;
}
.task{
  display: flex;
  justify-content: space-between;
  background-color: #390D02;
  border-radius: 3px;
  margin-bottom: 1px;
  padding: 2px 2px 1px 6px;
}

.task:hover{
  background-color: #4C4A59;
}
.container{
  color:#F2CDAC;
  padding: 6px 12px;
  background-color: #103778;
  border-radius: 8px;
  max-width: 420px;
  margin: 0 auto;
  font-family: 'Edu TAS Beginner', cursive;
}

.subtitle{
  font-size: 10px;
  margin: 0;
  margin-bottom: 16px;
  text-align: center;
  opacity: 0.6;
}

h1{
  text-transform: uppercase;
  font-size: 18px;
  text-align: center;
  margin: 0;
  margin-top: 12px;

}
</style>
