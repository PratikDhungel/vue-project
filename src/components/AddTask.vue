<template>
  <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" v-model="text" name="text" placeholder="Add Task" />
      <label v-if="errors.text" class="error">{{ errors.text }}</label>
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
        type="text"
        v-model="day"
        name="day"
        placeholder="Add Day & Time"
      />
      <label v-if="errors.day" class="error">{{ errors.day }}</label>
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input type="checkbox" v-model="reminder" name="reminder" />
    </div>

    <button type="submit" class="btn btn-block">Save Task</button>
  </form>
</template>

<script>
export default {
  name: 'AddTask',
  data() {
    return {
      text: '',
      day: '',
      reminder: false,
      errors: {
        text: '',
        day: '',
      },
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()

      if (!this.text || !this.day) {
        if (!this.text) this.errors.text = 'Required'
        if (!this.day) this.errors.day = 'Required'
      } else {
        const newTask = {
          id: Math.floor(Math.random() * 1000000),
          text: this.text,
          day: this.day,
          reminder: this.reminder,
        }

        this.$emit('add-task', newTask)
      }
    },
  },
  watch: {
    text(newText) {
      if (newText) {
        this.errors.text = ''
      }
      if (newText === '') {
        this.errors.text = 'Required'
      }
    },
    day(newDay) {
      if (newDay) {
        this.errors.day = ''
      }
      if (newDay === '') {
        this.errors.day = 'Required'
      }
    },
  },
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 16px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}

.error {
  margin-left: 5px;
  font-size: 13px;
  color: red;
}
</style>
