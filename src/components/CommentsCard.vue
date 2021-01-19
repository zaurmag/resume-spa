<template>
  <div class="card">
    <h2>{{ commentsTitle }}</h2>
    <ul class="list">
      <li v-for="item in commentsData" :key="item.id" class="list-item">
        <div>
          <p><strong>{{ item.email }}</strong></p>
          <small>{{ item.body }}</small>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
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
  name: 'CommentsCard'
}
</script>
