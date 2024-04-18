<template>
    <main>
        <section class="movie-section">
            <div class="container">
                <h2>Film</h2>
            </div>
            <div class="container">
                <ul>
                    <card v-for="movie in store.movies" :key="movie.id" :item="movie" />
                </ul>

            </div>

        </section>
        <section class="series-section">
            <div class="container">
                <h2>Serie TV</h2>
            </div>
            <div class="container">
                <ul>
                    <card v-for="serie in store.series" :key="serie.id" :item="serie" />
                </ul>
            </div>

        </section>
    </main>
</template>

<script>
import card from './appCard.vue';

import { store } from '../store.js';

export default {
    components: {
        card,
    },
    data() {
        return {
            store: store
        }
    }
}

</script>

<style lang="scss" scoped></style>