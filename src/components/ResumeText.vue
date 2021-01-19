<template>
  <p>{{ value }}</p>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: '',
      required: true
    }
  },
  name: 'ResumeText'
}
</script>
