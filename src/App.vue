<template>
  <div class="container column">
    <app-form @block-added="addData"></app-form>
    <app-resume :resumeData="resumeData"></app-resume>
  </div>
  <div class="container">
    <app-loader v-if="loader"></app-loader>
    <comments-card
      v-else
      @load-comments="loadComments"
      :comments-data="comments"
      comments-title="Комментарии"
    ></comments-card>
  </div>
</template>

<script>
import AppForm from '@/components/AppForm/AppForm'
import AppResume from '@/components/AppResume'
import CommentsCard from '@/components/CommentsCard'
import AppLoader from '@/components/AppLoader'
import axios from 'axios'

export default {
  data () {
    return {
      resumeData: [],
      comments: [],
      loader: false
    }
  },
  methods: {
    async getResume () {
      try {
        const { data } = await axios.get('https://course-summary-default-rtdb.firebaseio.com/resume.json')
        this.resumeData = Object.keys(data).map(key => {
          return {
            ...data[key]
          }
        })
      } catch (e) {
        console.error(e.message)
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
        console.error(e.message())
        this.loader = false
      }
    },
    addData (value) {
      this.resumeData.push(value)
    }
  },
  mounted () {
    this.getResume()
  },
  components: {
    AppForm,
    AppResume,
    CommentsCard,
    AppLoader
  }
}
</script>
