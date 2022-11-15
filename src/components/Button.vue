<template>
  <button @click="onClick" :style="{ background: color }" class="btn">
    {{ label }}
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: ['label', 'color'],
  methods: {
    onClick() {
      this.$emit('on-click')
    },
  },
  emits: ['on-click'],
}
</script>
