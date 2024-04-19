<template>
    <header class="header bg-black">
        <div class="container bg-black">
            <div class="row bg-black ">
                <img class="logo bg-black" src="/public/logo.png" alt="">
                <div class="search-tab bg-black">
                    <input class="search-bar" type="text" v-model="query" placeholder="Scrivi il titolo che cerchi"
                        @keyup.enter="getAll">
                    <button class="search-btn" @click="getAll">cerca</button>
                </div>

            </div>

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
                    this.store.movies = res.data.results.map(movie => ({
                        title: movie.title,
                        original_title: movie.original_title,
                        original_language: movie.original_language,
                        vote_average: movie.vote_average,
                        rating: calculateRating(movie.vote_average),
                        id: movie.id,
                        poster: `https://image.tmdb.org/t/p/w185${movie.poster_path}`,
                        flag: getFlag(movie)
                    }))
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
                    this.store.series = res.data.results.map(serie => ({
                        title: serie.name,
                        original_title: serie.original_name,
                        original_language: serie.original_language,
                        vote_average: serie.vote_average,
                        rating: calculateRating(serie.vote_average),
                        id: serie.id,
                        poster: `https://image.tmdb.org/t/p/w185${serie.poster_path}`,
                        flag: getFlag(serie)
                    }))
                })

            console.log('recupero i dati di serie tv')
        }

    }
}

function calculateRating(vote) {
    return Math.floor(vote / 2) + 1;
}

function getFlag(item) {
    let code = item.origin_country && item.origin_country.length ? item.origin_country[0] : item.original_language

    if (code == "en") {
        code = "us";
    }

    return `https://flagsapi.com/${code.toUpperCase()}/flat/32.png`

}

</script>

<style lang="scss" scoped>
.bg-black {
    background-color: black;
}


.logo {
    cursor: pointer;
}




.search-bar {
    height: 30px;
    background-color: white;
    border: none;
    border-radius: 10px;
}

.search-btn {
    height: 30px;
    width: 50px;
    background-color: red;
    color: white;
    border: none;
    border-radius: 10px;
}

.search-tab {
    width: 40%;
    display: flex;
    justify-content: center;
    gap: 10px;
    align-items: center;
}
</style>
