<template>
  <div>
    <div class="container column">
      <app-resume-window @submit="updateResume"></app-resume-window>
      <app-resume
        :title="title"
        :avatar="avatar"
        :subText="subText"
        :resumeBlocks="resumeBlocks"
        @update="update"
      ></app-resume>
    </div>
    <div class="container">
      <p>
        <button class="btn primary" @click="loadComments" v-if="!comments.length">Загрузить комментарии</button>
      </p>
      <app-loader v-if="loadingComments"></app-loader>
      <app-comments :comments="comments" v-if="comments.length"></app-comments>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import AppResumeWindow from '@/components/AppResumeWindow'
import AppComments from '@/components/AppComments'
import AppResume from '@/components/AppResume'
import AppLoader from '@/components/AppLoader'

export default {
  name: 'App',
  data: () => ({
    loadingComments: false,
    loadingResume: true,
    title: null,
    avatar: null,
    subText: null,
    resumeBlocks: [],
    comments: []
  }),
  computed: {},
  methods: {
    async update(type, value) {
      this[type] = value
    },
    async updateResume({type, value}) {
      try {
        if (type !== 'windows') {
          this[type] = value
          this.title = value
          this.subText = value
        } else {
          this.resumeBlocks.push(value)
        }
      } catch (e) {}
    },
    async loadComments() {
      this.loadingComments = true
      try {
        const url = 'https://jsonplaceholder.typicode.com/comments'
        const {data} = await axios.get(url, {params: {_limit: 42}})
        if (data) {
          this.comments = data
          this.loadingComments = false
        }
      } catch (e) {
      }
    },

  },
  async mounted() {
    await this.loadResume()
  },
  components: {AppResumeWindow, AppResume, AppComments, AppLoader}
}
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
