<template>
    <main class="container">
        <div class=" my-4 gy-4 d-flex justify-content-between">
            <div v-if="this.data.current_page > 1" type="button" class="d-flex gap-3">
                <button @click="first_page" class="btn btn-primary">PRIMA PAGINA</button>
                <button @click="previous_page" class="btn btn-primary">INDIETRO</button>
            </div>
            <div>
                <h3>Page:{{ this.data.current_page }}</h3>
            </div>
            <div v-if="!(this.data.last_page === this.data.current_page)" class="d-flex gap-3">
                <button @click="next_page" type="button" class="btn btn-primary">AVANTI</button>
                <button @click="last_page" class="btn btn-primary">ULTIMA PAGINA</button>
            </div>
            <!-- v-if="this.data.current_page === this.data.last_page" -->
        </div>
        <div class="row my-2 gy-2">
            <div v-for="project in data.data" class="col col-md-4">
                <AppCard :image="project.image" :title="project.title" :description="project.description" />
            </div>
        </div>
    </main>
</template>

<script>
import AppCard from './AppCard.vue';

export default {
    name: "AppMain",
    props: {
        data: Object
    },
    components: { AppCard },

    methods: {
        previous_page() {
            this.$emit('previous_page');
        },
        next_page() {
            this.$emit('next_page');
        },
        first_page() {
            this.$emit('first_page')
        },
        last_page() {
            this.$emit('last_page')
        }
    },
}

</script>
