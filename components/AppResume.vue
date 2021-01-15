<template>
  <div class="card card-w70">
    <app-resume-title v-if="title" :title="title" @update="$emit('update', 'title', $event)"></app-resume-title>
    <app-resume-avatar v-if="avatar" :avatar="avatar"></app-resume-avatar>
    <div v-for="(resumeBlock, idx) in resumeBlocks" :key="resumeBlock.id">
      <app-resume-subtitle
                 :subtitle="resumeBlock.subtitle"
                 :idx="idx"
                 :resume-blocks-length="resumeBlocks.length"
      >
      </app-resume-subtitle>
      <app-resume-text>{{ resumeBlock.text }}</app-resume-text>
    </div>
    <h3 v-if="isEmptyResume">Добавьте первый блок, чтобы увидеть результат</h3>
  </div>
</template>

<script>
import AppResumeTitle from '@/components/AppResumeTitle'
import AppResumeAvatar from '@/components/AppResumeAvatar'
import AppResumeSubtitle from '@/components/AppResumeSubtitle'
import AppResumeText from '@/components/AppResumeText'

export default {
  name: 'AppResumeContent',
  emits: ['update'],
  props: {
    title: String,
    avatar: String,
    resumeBlocks: Array
  },
  computed: {
    isEmptyResume() {
      return !this.title && !this.avatar && this.resumeBlocks.length === 0
    }
  },
  components: {AppResumeTitle, AppResumeAvatar, AppResumeSubtitle, AppResumeText}
}
</script>
