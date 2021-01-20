<template>
  <form class="card card-w30" v-on:submit.prevent="formSubmit">
    <form-field-select
      label="Тип блока"
      name="type"
      v-model:value="type"
      :options="options"
    ></form-field-select>

    <form-field-textarea
      label="Значение"
      name="value"
      v-model:value="value"
    ></form-field-textarea>

    <app-btn color="primary" :isDisabled="value.length < 3">Добавить</app-btn>
  </form>
</template>

<script>
import FormFieldSelect from '@/components/AppForm/FormFieldSelect'
import FormFieldTextarea from '@/components/AppForm/FormFieldTextarea'
import AppBtn from '@/components/AppBtn'

export default {
  data () {
    return {
      type: 'title',
      value: '',
      options: [
        {
          title: 'Заголовок',
          value: 'title'
        },
        {
          title: 'Подзаголовок',
          value: 'subtitle'
        },
        {
          title: 'Автар',
          value: 'avatar'
        },
        {
          title: 'Текст',
          value: 'text'
        }
      ]
    }
  },
  emits: ['block-added'],
  methods: {
    async formSubmit () {
      await fetch('https://course-summary-default-rtdb.firebaseio.com/resume.json', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          type: this.type,
          value: this.value
        })
      })
      this.$emit('block-added', {
        id: Date.now(),
        type: this.type,
        value: this.value
      })

      this.type = 'title'
      this.value = ''
    }
  },
  components: {
    FormFieldSelect,
    FormFieldTextarea,
    AppBtn
  }
}
</script>

<style scoped>

</style>
