<template>
  <div class="container column">
    <form class="card card-w30" v-on:submit.prevent="formSubmit">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" name="type" v-model="type">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>
      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" name="value" v-model="value"></textarea>
      </div>
      <app-btn color="primary" :isDisabled="false">Добавить</app-btn>
    </form>

    <loader v-if="loader"></loader>
    <div class="card card-w70" v-else>
      <component :is="`resume-${item.type}`" v-for="item in resumeData" :key="item" :value="item.value"></component>
    </div>
  </div>
  <div class="container">
    <p>
      <app-btn color="warning">Загрузить комментарии</app-btn>
    </p>
    <comments-card></comments-card>
  </div>
</template>

<script>
// import FormFieldType from '@/components/FormFieldType'
// import FormFieldValue from '@/components/FormFieldValue'
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
      type: '',
      value: '',
      resumeData: [],
      loader: false
    }
  },
  methods: {
    async formSubmit () {
      this.loader = true
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
      this.value = ''
      this.loader = false
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
    }
  },
  computed: {
  },
  mounted () {
    this.getResume()
  },
  components: {
    // FormFieldType,
    // FormFieldValue,
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
