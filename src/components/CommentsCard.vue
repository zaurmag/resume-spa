<template>
  <div class="card">
    <h2>Комментарии</h2>
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
  props: ['commentsData'],
  name: 'CommentsCard'
}
</script>
