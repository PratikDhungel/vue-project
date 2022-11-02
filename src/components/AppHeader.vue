<template>
  <header>
    <h1>{{ title }}</h1>
    <Button label="Add Text" color="green" />
  </header>
</template>

<script>
import Button from './Button.vue'

export default {
  name: 'AppHeader',
  props: ['title'],
  components: {
    Button,
  },
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
