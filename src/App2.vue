<script setup>
import { ref, onMounted } from 'vue'

const name = ref('John');
const status = ref('active');
const tasks = ref(['task 1', 'task 2', 'task 3']);
const link = ref('https://www.google.com');
const toggleStatus = () => {
if (status.value === 'active') {
  status.value = 'inactive'
} else if (status.value === 'inactive')  {
  status.value = 'active'
  } else {
    status.value = 'unknown'
  }
};
const newTask = ref('');
const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  } else {
    alert('Please enter a task');
  }
};
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map(task => task.title);
  } catch (error) {
    console.error('Error fetching tasks:', error);
  }
});
</script> 


<template>
  <h1> {{ name }} </h1>
  <p v-if="status === 'active'">Status: Active</p>
  <p v-else-if="status === 'inactive'">Status: Inactive</p>
  <p v-else>Status: Unknown</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task:</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask" placeholder="Add a new task" />
    <button type="submit">Add Task</button>
  </form>


  <h3>Tasks</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task"> 
      <span>
      {{ task }} 
      </span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>

  <br />
  <button @click="toggleStatus">Change Status</button>

</template>



