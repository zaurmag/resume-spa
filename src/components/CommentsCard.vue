<template>
  <div class="card">
    <h2>{{ commentsTitle }}</h2>
    <ul class="list">
      <li
        v-for="item in commentsData"
        :key="item.id"
        class="list-item"
      >
        <div>
          <p><strong>{{ item.email }}</strong></p>
          <small>{{ item.body }}</small>
        </div>
      </li>
    </ul>
  </div>
  <p>
    <app-btn color="primary" @action="$emit('load-comments')">Загрузить комментарии</app-btn>
  </p>
</template>

<script>
import AppBtn from '@/components/AppBtn'

export default {
  emits: ['load-comments'],
  props: {
    commentsData: {
      type: Array,
      required: true
    },
    commentsTitle: {
      type: String,
      required: true,
      default: 'Комментарии'
    }
  },
  components: {
    AppBtn
  }
}
</script>
