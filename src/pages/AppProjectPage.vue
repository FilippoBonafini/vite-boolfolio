<template>
    <div class="container my-5">
        <h1>{{ project.title }}</h1>
        <p>{{ project.description }}</p>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'ProjectPage',
    data() {
        return {
            apiBaseUrl: 'http://127.0.0.1:8000/api/',
            apiUrls: {
                projects: 'projects'
            },
            project: null
        }
    },
    methods: {
        getProject() {
            axios.get(this.apiBaseUrl + this.apiUrls.projects + '/' + this.$route.params.slug)
                .then((response) => {
                    this.project = response.data.results
                })
                .catch((error) => {
                    console.log(error)
                })
        }
    },
    created() {
        this.getProject()
    }
}
</script>

