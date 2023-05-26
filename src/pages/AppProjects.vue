<template>
    <main class="container">
        <div class=" my-4 gy-4 d-flex justify-content-between">
            <div v-if="this.projects.current_page > 1" type="button" class="d-flex gap-3">
                <button @click="getProjects(first_page_url)" class="btn btn-primary">PRIMA PAGINA</button>
                <button @click="getProjects(previous_page_url)" class="btn btn-primary">INDIETRO</button>
            </div>
            <div>
                <h3>Page:{{ this.projects.current_page }}</h3>
            </div>
            <div v-if="!(this.projects.last_page === this.projects.current_page)" class="d-flex gap-3">
                <button @click="getProjects(next_page_url)" type="button" class="btn btn-primary">AVANTI</button>
                <button @click="getProjects(last_page_url)" class="btn btn-primary">ULTIMA PAGINA</button>
            </div>
        </div>
        <div class="row my-2 gy-4">
            <div v-for="project in projects.data" class="col col-md-4">
                <AppCard :image="project.image" :title="project.title" :description="project.description" />
            </div>
        </div>
    </main>
</template>

<script>
import axios from 'axios';
import AppCard from '../components/AppCard.vue';

export default {
    name: "AppMain",

    components: { AppCard },

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

}

</script>
