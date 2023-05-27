<!-- <template>
    <main class="container pt-4">
        <div class="d-flex justify-content-between">
            <div class="d-flex gap-3">
                <button :disabled="this.projects.current_page === 1" @click="getProjects(first_page_url)"
                    class="btn btn-primary">PRIMA PAGINA</button>
                <button :disabled="this.projects.current_page === 1" @click="getProjects(previous_page_url)"
                    class="btn btn-primary">INDIETRO</button>
            </div>
            <div class="d-flex text-center">
                <h3>Page: {{ this.projects.current_page }}</h3>
            </div>
            <div class="d-flex gap-3">
                <button :disabled="this.projects.last_page === this.projects.current_page"
                    @click="getProjects(next_page_url)" type="button" class="btn btn-primary">AVANTI</button>
                <button :disabled="this.projects.last_page === this.projects.current_page"
                    @click="getProjects(last_page_url)" class="btn btn-primary">ULTIMA PAGINA</button>
            </div>
        </div>
        <div class="row my-2 gy-4 col">
            <div v-for="project in projects.data" class="col col-md-4">
                <AppCard :image="project.image" :title="project.title" :slug="project.slug"
                    :description="project.description" />
            </div>
        </div>
    </main>
</template> -->
<template>
    <main class="container pt-4">
        <div class="row my-2 gy-4 col">
            <div v-for="project in projects.data" class="col col-md-4">
                <AppCard :image="project.image" :title="project.title" :slug="project.slug"
                    :description="project.description" />
            </div>
            <div v-if="this.loadStatus === true" class="mb-4 d-flex justify-content-center">
                <div class="spinner-border" role="status">
                    <span class="visually-hidden">Loading...</span>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
import axios from 'axios';
import AppCard from '../components/AppCard.vue';

export default {
    name: "AppProjects",
    components: { AppCard },
    data() {
        return {
            apiBaseUrl: 'http://127.0.0.1:8000/api/',
            apiUrls: {
                projects: 'projects'
            },
            // first_page_url: '',
            // last_page_url: '',
            // next_page_url: '',
            // previous_page_url: '',
            projects: [],
            loadStatus: null
        }
    },
    created() {
        window.addEventListener('scroll', this.handleScroll);
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
                if (this.next_page_url) {
                    this.loadStatus = true
                }
            }).catch((error) => {
                console.log(error)
            })
        },

        handleScroll() {
            const scrollPosition = window.innerHeight + window.scrollY;
            const documentHeight = document.documentElement.offsetHeight;

            if (scrollPosition >= documentHeight) {
                clearTimeout(this.scrollTimeout);
                this.scrollTimeout = setTimeout(this.loadNextPage, 300); // Ritardo di 1 secondo (1000 millisecondi)
            }
        },


        loadNextPage() {
            if (this.next_page_url) {
                this.loadStatus = true
                axios.get(this.next_page_url)
                    .then((response) => {
                        this.projects.data = this.projects.data.concat(response.data.results.data);
                        this.next_page_url = response.data.results.next_page_url;
                    })
                    .catch((error) => {
                        console.log(error);
                    });
            } else {
                this.loadStatus = false
            }
        },
    },
}
</script>
