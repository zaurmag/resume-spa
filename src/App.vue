<template>
  <div class="container column">
    <form class="card card-w30" v-on:submit.prevent="formSubmit">
      <form-field-type></form-field-type>
      <form-field-value></form-field-value>
      <app-btn color="primary" :isDisabled="false">Добавить</app-btn>
    </form>

    <div class="card card-w70">
      <resume-title>Заголовок</resume-title>
      <resume-avatar></resume-avatar>
      <resume-subtitle>Подзаголовок</resume-subtitle>
      <resume-text></resume-text>
    </div>
  </div>
  <div class="container">
    <p>
      <app-btn color="warning">Загрузить комментарии</app-btn>
    </p>
    <comments-card></comments-card>
    <loader></loader>
  </div>
</template>

<script>
import FormFieldType from '@/components/FormFieldType'
import FormFieldValue from '@/components/FormFieldValue'
import AppBtn from '@/components/AppBtn'
import CommentsCard from '@/components/CommentsCard'
import Loader from '@/components/Loader'
import ResumeTitle from '@/components/ResumeTitle'
import ResumeSubtitle from '@/components/ResumeSubtitle'
import ResumeAvatar from '@/components/ResumeAvatar'
import ResumeText from '@/components/ResumeText'

export default {
  data () {
    return {
      resumeData: []
    }
  },
  methods: {
    formSubmit (event) {
      // https://course-summary-default-rtdb.firebaseio.com/
      console.log(event)
    }
  },
  components: {
    FormFieldType,
    FormFieldValue,
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

<style>
  .avatar {
    display: flex;
    justify-content: center;
  }

  .avatar img {
    width: 150px;
    height: auto;
    border-radius: 50%;
  }
</style>
