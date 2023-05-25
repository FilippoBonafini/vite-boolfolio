<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import AppFooter from './components/AppFooter.vue';

export default {
  name: 'App',
  data() {
    return {
      apiBaseUrl: 'http://127.0.0.1:8000/api/',
      apiUrls: {
        projects: 'projects'
      },
      next_page_url: '',
      previous_page_url: '',
      projects: []
    }
  },
  created() {
    this.getProjects(this.apiUrls.projects)
  },
  methods: {
    getProjects(url) {
      axios.get(this.apiBaseUrl + url).then((response) => {
        this.projects = response.data.results;
        this.next_page_url = response.data.results.next_page_url
        if (response.data.results.prev_page_url) {
          this.previous_page_url = response.data.results.prev_page_url
        }
      }).catch((error) => {
        console.log(error)
      })
    },
    previous_page() {
      axios.get(this.previous_page_url).then((response) => {
        this.projects = response.data.results;
        this.next_page_url = response.data.results.next_page_url
        if (response.data.results.prev_page_url) {
          this.previous_page_url = response.data.results.prev_page_url
        }
      }).catch((error) => {
        console.log(error)
      })
    },
    next_page() {
      axios.get(this.next_page_url).then((response) => {
        this.projects = response.data.results;
        this.next_page_url = response.data.results.next_page_url
        if (response.data.results.prev_page_url) {
          this.previous_page_url = response.data.results.prev_page_url
        }
      }).catch((error) => {
        console.log(error)
      })
    }
  },
  components: {
    AppHeader,
    AppMain,
    AppFooter
  }
}
</script>

<template>
  <AppHeader />
  <AppMain :data="projects" @previous_page="previous_page" @next_page="next_page" />
  <AppFooter />
</template>


<style lang="scss">
//versione 1 - inclusione via app.vue
// @use './assets/scss/main.scss' as *;
</style>
