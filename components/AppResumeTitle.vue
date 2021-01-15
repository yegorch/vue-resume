<template>
  <h1>{{ title }} </h1>
</template>

<script>
export default {
  name: 'AppResumeTitle',
  props: ['title']
}
</script>

<style scoped>
h1 {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

img {
  width: 20px;
  
}

</style>
