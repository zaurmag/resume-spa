<template>
  <div class="form-control">
    <label :for="id">{{ label }}</label>
    <select :id="id" :name="name" @change="change" :value="value">
      <option v-for="option in options" :key="option" :value="option.value">{{ option.title }}</option>
    </select>
  </div>
</template>

<script>
export default {
  emits: ['update:value'],
  props: {
    options: {
      type: Array,
      required: true
    },
    value: String,
    label: {
      type: String,
      default: '',
      required: true
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
