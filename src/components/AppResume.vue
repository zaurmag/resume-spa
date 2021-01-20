<template>
  <div class="card card-w70">
    <template v-if="resumeData.length">
      <component
        v-for="block in resumeData"
        :is="`resume-${block.type}`"
        :key="block"
        v-bind="{value: block.value}"
      ></component>
    </template>
    <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>

<script>
import ResumeTitle from '@/components/ResumeBlocks/ResumeTitle'
import ResumeAvatar from '@/components/ResumeBlocks/ResumeAvatar'
import ResumeSubtitle from '@/components/ResumeBlocks/ResumeSubtitle'
import ResumeText from '@/components/ResumeBlocks/ResumeText'

export default {
  props: ['resumeData'],
  components: {
    ResumeTitle,
    ResumeAvatar,
    ResumeSubtitle,
    ResumeText
  }
}
</script>
