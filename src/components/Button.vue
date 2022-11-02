<template>
  <button :style="{ background: color }" class="btn">{{ label }}</button>
</template>

<script>
export default {
  name: 'Button',
  props: ['label', 'color'],
}
</script>
