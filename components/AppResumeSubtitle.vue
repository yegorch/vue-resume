<template>
  <h2>
    {{ subtitle }}
  </h2>

</template>

<script>


export default {
  name: 'AppResumeSubtitle',
  props: ['subtitle', 'resumeBlocksLength', 'idx'],
}
</script>

