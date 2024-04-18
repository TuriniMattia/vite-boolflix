<template>
    <header>
        <div class="container">
            <input type="text" v-model="query" placeholder="Scrivi il titolo che cerchi">
            <button @click="getAll">Scrivi il titolo che cerchi</button>
        </div>
    </header>
</template>

<script>
import axios from 'axios';
import { store } from "../store.js";

export default {
    data() {

        return {
            query: '',
            store: store,
        }
    },
    methods: {
        getAll() {
            this.featchMovies();
            this.featchSeries()
        },
        featchMovies() {
            axios.get('https://api.themoviedb.org/3/search/movie',
                {
                    params: {
                        api_key: '10405ecc775b251611b45643a962ad49',
                        query: this.query,
                    },
                }).then((res) => {
                    this.store.movies = res.data.results
                })

            console.log('recupero i dati di film')
        },
        featchSeries() {
            axios.get('https://api.themoviedb.org/3/search/tv',
                {
                    params: {
                        api_key: '10405ecc775b251611b45643a962ad49',
                        query: this.query,
                    },
                }).then((res) => {
                    this.store.series = res.data.results
                })

            console.log('recupero i dati di serie tv')
        }

    }



}




</script>

<style lang="scss" scoped></style>