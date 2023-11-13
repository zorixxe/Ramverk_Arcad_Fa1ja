<template>
    <div>
      <h1>To-Do List</h1>
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          {{ task.text }}
          <button @click="removeTask(index)">Delete</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        newTask: "",
        tasks: []
      };
    },
    methods: {
      addTask() {
        if (this.newTask.trim() === "") return;
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = "";
      },
      removeTask(index) {
        this.tasks.splice(index, 1);
      }
    }
  };
  </script>