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
    async addTask(newTask) {
      const addRes = await fetch('http://localhost:5000/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(newTask),
      })

      const data = await addRes.json()

      this.tasks = [...this.tasks, data]
    },
    toggleAddForm() {
      this.showAddTask = !this.showAddTask
    },
    async deleteTask(id) {
      const delRes = await fetch(`http://localhost:5000/tasks/${id}`, {
        method: 'DELETE',
      })

      const status = delRes.status

      if (status === 200) {
        const filteredTasks = this.tasks.filter((task) => task.id !== id)
        this.tasks = filteredTasks
      } else {
        alert('Something went wrong!')
      }
    },
    async toggleReminder(task) {
      const currentTask = { ...task }
      const { id } = currentTask

      const updatedValue = { ...currentTask, reminder: !currentTask.reminder }

      const toggleRes = await fetch(`http://localhost:5000/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updatedValue),
      })

      const status = toggleRes.status

      if (status === 200) {
        const updatedTasks = this.tasks.map((task) =>
          task.id === id ? updatedValue : task,
        )
        this.tasks = updatedTasks
      } else {
        alert('Something went wrong')
      }
    },

    async fetchTasks() {
      const response = await fetch('http://localhost:5000/tasks')

      const data = await response.json()

      return data
    },
  },
  async created() {
    const tasks = await this.fetchTasks()

    this.tasks = tasks
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
