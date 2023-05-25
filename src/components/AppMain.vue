<template>
    <main class="container">
        <div class="row my-4 gy-4">
            <div v-for="project in data" class="col col-md-4">
                <div class="card">
                    <img src="..." class="card-img-top" alt="...">
                    <div class="card-body">
                        <h5 class="card-title">{{ project.title }}</h5>
                        <p class="card-text">{{ project.description }}</p>
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