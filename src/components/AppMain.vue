<template>
    <main class="container">
        <div class="row my-4 gy-4">
            <div v-for="project in data" class="col col-md-4">
                <div class="card">
                    <img v-if="project.image" :src="project.image" class="card-img-top" alt="...">
                    <div class="card-body">
                        <h5 class="card-title">{{ project.title }}</h5>
                        <p v-if="project.description" class="card-text">{{ project.description.substring(0,
                            this.contentLenght) }}</p>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
export default {
    name: 'AppMain',
    props: {
        data: Object
    }
}
</script>

<style></style>