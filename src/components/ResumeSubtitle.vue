<template>
  <h2>{{ value }}</h2>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: '',
      required: false
    }
  },
  name: 'ResumeSubtitle'
}
</script>
