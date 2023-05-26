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
      first_page_url: '',
      last_page_url: '',
      next_page_url: '',
      previous_page_url: '',
      projects: []
    }
  },
  created() {
    this.getProjects((this.apiBaseUrl + this.apiUrls.projects))
  },
  methods: {
    getProjects(url) {
      axios.get(url).then((response) => {
        this.projects = response.data.results;
        // SE L'URL DELLA PRIMA PAGINA NON E' STATO SETTATO... SETTALO 
        this.first_page_url = !this.first_page_url ? response.data.results.first_page_url : this.first_page_url;

        // SE L'URL DELL'ULTIMA PAGINA NON E' STATO SETTATO... SETTALO 
        this.last_page_url = !this.last_page_url ? response.data.results.last_page_url : this.last_page_url;

        // SETTA L'URL DELLA PROSSIMA PAGINA 
        this.next_page_url = response.data.results.next_page_url

        // SE E' PRESENTE NEI RISULTATI, SETTA L'URL DELLA PAGINA PRECEDENTE 
        this.previous_page_url = response.data.results.prev_page_url ? response.data.results.prev_page_url : this.previous_page_url;
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
  <AppMain :data="projects" @previous_page="getProjects(previous_page_url)" @next_page="getProjects(next_page_url)"
    @first_page="getProjects(first_page_url)" @last_page="getProjects(last_page_url)" />
  <AppFooter />
</template>
