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
  <AppMain :data="projects" />
  <AppFooter />
</template>


<style lang="scss">
//versione 1 - inclusione via app.vue
// @use './assets/scss/main.scss' as *;
</style>
