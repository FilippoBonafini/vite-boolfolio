<template>
    <main class="container">
        <div class=" my-4 gy-4 d-flex justify-content-between">
            <div><button @click="previous_page" v-if="this.data.current_page > 1" type="button"
                    class="btn btn-primary">INDIETRO</button></div>
            <div>
                <h3>Page:{{ this.data.current_page }}</h3>
            </div>
            <div><button @click="next_page" type="button" class="btn btn-primary">AVANTI</button></div>
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
        }
    },
}

</script>
