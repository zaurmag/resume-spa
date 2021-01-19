<template>
  <div class="container column">
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

    <div class="card card-w70">
      <h3 v-if="resumeData.length === 0">Добавьте первый блок, чтобы увидеть результат</h3>
      <component v-else :is="`resume-${item.type}`" v-for="item in resumeData" :key="item" :value="item.value"></component>
    </div>
  </div>
  <div class="container">
    <p>
      <app-btn color="warning" @action="loadComments">Загрузить комментарии</app-btn>
    </p>
    <loader v-if="loader"></loader>
    <comments-card :comments-data="comments" comments-title="Комментарии" v-else></comments-card>
  </div>
</template>

<script>
import FormFieldSelect from '@/components/FormFieldSelect'
import FormFieldTextarea from '@/components/FormFieldTextarea'
import AppBtn from '@/components/AppBtn'
import CommentsCard from '@/components/CommentsCard'
import Loader from '@/components/Loader'
import ResumeTitle from '@/components/ResumeTitle'
import ResumeSubtitle from '@/components/ResumeSubtitle'
import ResumeAvatar from '@/components/ResumeAvatar'
import ResumeText from '@/components/ResumeText'
import axios from 'axios'

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
      ],
      resumeData: [],
      loader: false,
      comments: []
    }
  },
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
      const type = this.type
      const value = this.value
      this.resumeData.push(
        {
          type,
          value
        }
      )
      this.type = 'title'
      this.value = ''
    },
    async getResume () {
      try {
        this.loader = true
        const { data } = await axios.get('https://course-summary-default-rtdb.firebaseio.com/resume.json')
        this.resumeData = Object.keys(data).map(key => {
          return {
            ...data[key]
          }
        })
        this.loader = false
      } catch (e) {
        console.error(e.message)
        this.loader = false
      }
    },
    async loadComments () {
      this.loader = true
      try {
        this.loader = true
        const { data } = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
        this.comments = Object.keys(data).map(key => {
          return {
            ...data[key]
          }
        })
        this.loader = false
      } catch (e) {
        console.warn(e.message())
        this.loader = false
      }
    }
  },
  mounted () {
    this.getResume()
  },
  components: {
    FormFieldSelect,
    FormFieldTextarea,
    AppBtn,
    CommentsCard,
    Loader,
    ResumeTitle,
    ResumeSubtitle,
    ResumeAvatar,
    ResumeText
  }
}
</script>
