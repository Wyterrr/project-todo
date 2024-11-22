<template>
  <div class="app-container">
    <h1 class="app-title">Project ToDoList</h1>
    <h6>By Wenene & Wyterrr</h6>
    <form class="task-form" @submit.prevent="addTasks">
      <input v-model="newTask" type="text" placeholder="Insérer une tâche à faire" />
      <button :disabled="newTask.length === 0">Ajouter</button>
    </form>

    <p v-if="tasks.length === 0" class="no-tasks">Vous n'avez pas de tâches à faire</p>

    <div v-else>
      <ul class="task-list">
        <li
          v-for="newTask in sortedTasks()"
          :key="newTask.date"
          :class="{ completed: newTask.completed }"
        >
          <label class="task-item">
            <div class="custom-checkbox">
              <input type="checkbox" v-model="newTask.completed" />
              <span></span>
            </div>
            <span class="task-title">{{ newTask.title }}</span>
            <button class="delete-btn" @click="deleteTask(newTask)">
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="delete-icon">
                <line x1="18" y1="6" x2="6" y2="18"></line>
                <line x1="6" y1="6" x2="18" y2="18"></line>
              </svg>
            </button>
          </label>
        </li>
      </ul>
      <label class="hide-completed">
        <div class="custom-checkbox">
          <input type="checkbox" v-model="hideCompleted" />
          <span></span>
        </div>
        Masquer les tâches complétées
      </label>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const tasks = ref([]);
const hideCompleted = ref(false);
const newTask = ref("");

const addTasks = () => {
  tasks.value.push({
    title: newTask.value,
    completed: false,
    date: Date.now(),
  });
  newTask.value = "";
};

const deleteTask = (taskToDelete) => {
  tasks.value = tasks.value.filter((task) => task !== taskToDelete);
};

const sortedTasks = () => {
  const sortedTasks = tasks.value.toSorted((a, b) =>
    a.completed > b.completed ? 1 : -1
  );
  if (hideCompleted.value) {
    return sortedTasks.filter((t) => !t.completed);
  }
  return sortedTasks;
};

const Pop = (newTask) => {

}

</script>

<style>
body {
  font-family: Arial, sans-serif;
  background-color: #383232; 
  color: #fff;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.app-container {
  width: 100%;
  max-width: 400px;
  padding: 20px;
  background-color: #000;
  box-shadow: 0 4px 8px rgba(255, 255, 255, 0.5);
}

h6{
  text-align: center;
}

.app-title {
  font-size: 2rem;
  font-weight: bold;
  text-align: center;
  margin-bottom: 20px;
}

.task-form {
  display: flex;
  gap: 10px;
}

.task-form input[type="text"] {
  flex: 1;
  padding: 10px;
  border: 1px solid #fff;
  background-color: transparent;
  color: #fff;
  outline: none;
}

.task-form button {
  padding: 10px 20px;
  background-color: #ff0; 
  border: none;
  cursor: pointer;
  color: #000;
}

.task-form button:disabled {
  background-color: #555;
  cursor: not-allowed;
}


.task-list {
  list-style: none;
  padding: 0;
  margin: 20px 0;
}

.task-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 0;
  border-bottom: 1px solid #555;
}

.task-title {
  flex: 1;
  margin-left: 10px;
}

.completed .task-title {
  opacity: 0.5;
  text-decoration: line-through;
}

.custom-checkbox {
  position: relative;
  display: inline-block;
  margin-right: 5px;
  width: 20px;
  height: 20px;
}

.custom-checkbox input[type="checkbox"] {
  opacity: 0;
  position: absolute;
  width: 100%;
  height: 100%;
  cursor: pointer;
}

.custom-checkbox span {
  position: absolute;
  top: 0;
  left: 0;
  width: 20px;
  height: 20px;
  border: 2px solid #fff;
  border-radius: 4px;
  background-color: transparent;
  transition: all 0.3s;
}

.custom-checkbox input[type="checkbox"]:checked + span {
  background-color: rgb(187, 187, 10); 
  border-color: rgb(187, 187, 10);
}

.custom-checkbox input[type="checkbox"]:checked + span::before {
  content: "✔";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: #000;
  font-size: 12px;
}

.delete-btn {
  background: none;
  border: none;
  color: #fff;
  cursor: pointer;
  padding: 5px;
}

.delete-btn:hover .delete-icon {
  stroke: rgb(187, 187, 10); 
}

.delete-icon {
  width: 20px;
  height: 20px;
}
</style>
