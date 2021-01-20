<template>
  <div class="form-control">
    <label :for="id">{{ label }}</label>
    <textarea
      :id="id"
      rows="3"
      :name="name"
      :value="value"
      @input="change"
    ></textarea>
  </div>
</template>

<script>
export default {
  emits: ['update:value'],
  props: {
    value: String,
    label: {
      type: String,
      required: true,
      default: 'Заголовок поля'
    },
    name: {
      name: {
        type: String,
        default: '',
        required: true
      }
    }
  },
  data () {
    return {
      id: 'field-' + Math.random()
    }
  },
  methods: {
    change (event) {
      this.$emit('update:value', event.target.value)
    }
  }
}
</script>
