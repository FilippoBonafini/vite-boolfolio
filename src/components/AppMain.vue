<template>
    <main class="container">
        <div class="row my-4 gy-4">
            <div v-for="project in data" class="col col-md-4">
                <AppCard :image="project.image" :title="project.title" :description="project.description" />
            </div>
        </div>
    </main>
</template>

<script>
import AppCard from './AppCard.vue';

export default {
    name: "AppMain",
    data() {
        return {
            contentLenght: 100
        };
    },
    props: {
        data: Object
    },
    components: { AppCard }
}
</script>
