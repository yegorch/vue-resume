<template>
  <div class="avatar">
        <img :src="avatar">
  </div>
</template>

<script>
export default {
  name: 'AppResumeAvatar',
  props: {
    avatar: {
      type: String,
      validator(value) {
        try {
          new URL(value)
          return true
        } catch (_) {
          return false
        }
      }
    }
  }
}
</script>

