<template>
  <button class="btn" :class="color" @click="$emit('action')" :disabled="isDisabled">
    <slot />
  </button>
</template>

<script>
export default {
  name: 'AppBtn',
  emits: ['action'],
  props: {
    color: {
      type: String,
      default: '',
      validator (value) {
        return ['', 'primary', 'warning', 'danger'].includes(value)
      }
    },
    isDisabled: {
      type: Boolean,
      default: false
    }
  }
}
</script>
