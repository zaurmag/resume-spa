<template>
   <div class="avatar">
    <img :src="value" alt="">
   </div>
</template>

<script>
export default {
  name: 'ResumeAvatar',
  props: ['value']
}
</script>
