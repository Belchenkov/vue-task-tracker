<template>
  <div class="container">
    <Header title="Task Tracker" />
    <AddTask @add-task="addTask" />
    <Tasks
        @delete-task="deleteTask"
        :tasks="tasks"
        @toggle-reminder="toggleReminder"
    />
  </div>
</template>

<script>
import Header from './components/Header';
import Tasks from './components/Tasks';
import AddTask from './components/AddTask';
import db from '../db.json';

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: db.tasks
    }
  },
  methods: {
    addTask(task) {
      this.tasks = [
          ...this.tasks,
          task
      ];
    },
    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map(task => task.id === id ? {...task, reminder: !task.reminder} : task);
    }
  }

}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Titillium Web', sans-serif;
}

.container {
  max-width: 680px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}

.mr-2 {
  margin-right: 2px;
}
</style>
