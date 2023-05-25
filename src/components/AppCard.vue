<template>
    <div class="card">
        <img v-if="image" :src="image" class="card-img-top" alt="...">
        <div class="card-body">
            <h5 class="card-title">{{ title }}</h5>
            <p v-if="description" class="card-text">{{ description.substring(0,
                this.contentLenght) }}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'AppCard',
    props: {
        image: String,
        title: String,
        description: String
    },
    data() {
        return {
            contentLenght: 100
        };
    }
}
</script>