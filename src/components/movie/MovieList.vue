<template>
    <h5>Listado de Películas</h5>
    <div class="movie-list">
        <div class="movie-grid">
            <div class="movie-item" v-for="movie in movies" :key="movie.id"> 
                <MovieItem :movie="movie" />
            
            </div>
        </div>
    </div>
</template>

<style>
.movie-grid{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 20px;
}
</style>

<script>

import axios from 'axios'

import MovieItem from 'components/movie/MovieItem.vue'

export default {
    name:"MovieList",
    components: {
        MovieItem
    },

    mounted(){
        this.getMovies()
    },

    methods:{
        getMovies(){
            var url = "https://api.themoviedb.org/3/discover/movie"
            //var token = JSON.parse(localStorage.getItem("userData")).token;
            var token = "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIwNjZjMGIxYzEwY2RjNjk2YTVmY2U1N2VlNTVlZTM4YyIsInN1YiI6IjY1NWMyOWM5NTM4NjZlMDExYzBhYTA1YyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.PJ7b8ufGg4WfIo-buozEIQyvlUMMQNfGajibFnTX9pA";
            var header = {
                headers:{
                    Authorization: "Bearer " + token
                }
            }
            axios.get(url, header)
            .then(response => {
                this.movies = response.data.results

            }).catch(error => {

                console.log("Error: "+ error)

            })
        }
    },

    data(){
        return{
            movies: [ ]
        }
    }
}

</script>