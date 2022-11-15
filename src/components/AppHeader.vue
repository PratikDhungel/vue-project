<template>
  <header>
    <h1>{{ title }}</h1>
    <Button
      @on-click="onToggleAddForm"
      :label="showAddTask ? 'Close' : 'Add Task'"
      color="green"
    />
  </header>
</template>

<script>
import Button from './Button.vue'

export default {
  name: 'AppHeader',
  props: {
    title: String,
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
  methods: {
    onToggleAddForm() {
      this.$emit('toggle-add-form')
    },
  },
  emits: ['toggle-add-form'],
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
