<script setup>
import { ref } from 'vue'

let newTask = ref('')
let taskList = ref([
  { text: 'Estudiar', done: false },
  { text: 'Dormir', done: true }
])

function addTask() {
  if (newTask.value.trim() === '') {
    newTask.value = ''
    return
  }

  taskList.value.push({
    text: newTask.value,
    done: false
  })

  newTask.value = ''
}

function remove(index) {
  taskList.value.splice(index, 1)
}

function setDone(index) {
  taskList.value[index].done = !taskList.value[index].done
}
</script>

<template>
  <div class="card">
    <h1>To-Do</h1>
    <p class="subtitle">{{ newTask }}</p>
    <div>
      <div
        v-for="(task, index) in taskList"
        :key="index"
        @click="setDone(index)"
        class="task"
        :class="{ done: task.done }"
      >
        {{ task.text }}<span @click="remove(index)" class="button">X</span>
      </div>
    </div>
    <div>
      <input
        v-model="newTask"
        @keypress.enter="addTask"
        type="text"
        placeholder="Escribe tu tarea..."
      />
      <p v-show="newTask != ''" class="help">Presiona "INTRO" para añadir la tarea.</p>
    </div>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

.card {
  --sky: #78c0e0;
  --celestial: #449dd1;
  --navy: #150578;
  --federal: #0e0e52;
  --violet: #3943b7;

  font-family: 'Dancing Script', cursive;
  font-size: 48px;

  background-color: var(--federal);
  color: white;

  max-width: 520px;
  border-radius: 8px;
  padding: 18px 16px;
}

h1 {
  text-transform: uppercase;
  text-align: center;
  padding: 0;
  margin: 0;
}

.subtitle {
  margin: 0;
  padding: 0;
  text-align: center;
  opacity: 0.6;
  margin-bottom: 16px;
}

.task {
  background-color: var(--celestial);
  border-radius: 4px;
  padding: 2px 8px;
  margin-bottom: 2px;

  display: flex;
  justify-content: space-between;
}

.task:hover {
  background-color: var(--sky);
}

.button {
  background-color: var(--federal);
  padding: 0 5px;
  border-radius: 4px;
  font-size: 32px;
  cursor: pointer;
  line-height: 57px;
}

.button:hover {
  background-color: var(--violet);
}

input {
  font-family: 'Dancing Script', cursive;
  width: 100%;
  box-sizing: border-box;
  border: none;
  outline: none;
  padding: 3px 6px;
  border-radius: 4px;
  font-size: 48px;
}

.help {
  margin: 15px 0 0 0;
  font-size: 20px;
  opacity: 0.4;
}
</style>
