<template>
  <div class="container">
    <AppHeader
      @toggle-add-form="toggleAddForm"
      title="Task Tracker"
      :showAddTask="showAddTask"
    />
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    AppHeader,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    addTask(newTask) {
      this.tasks = [...this.tasks, newTask]
    },
    deleteTask(id) {
      const filteredTasks = this.tasks.filter((task) => task.id !== id)
      this.tasks = filteredTasks
    },
    toggleReminder(id) {
      const updatedTasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task,
      )
      this.tasks = updatedTasks
    },
    toggleAddForm() {
      this.showAddTask = !this.showAddTask
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'Nov 5, 2022 at 3:00 pm',
        reminder: true,
      },
      {
        id: 2,
        text: 'Meeting at School',
        day: 'Nov 2, 2022 at 11:00 am',
        reminder: false,
      },
    ]
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 500px;
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
</style>
