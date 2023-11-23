<template>
    <h5>Listado de Películas Favoritas</h5>
    <div class="favorite-list">
        <div class="favorite-grid" >
            <div class="favorite-item" v-for="favorite in favorites" :key="favorite.id"> 
                <FavoriteItem :favorite="favorite" />
            
            </div>
        </div>
    </div>
</template>

<style>
.favorite-grid{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 20px;
}
</style>

<script>

import axios from 'axios'

import FavoriteItem from 'components/favorite/FavoriteItem.vue'

export default {
    name:"FavoriteList",
    components: {
        FavoriteItem
    },

    mounted(){
        this.getFavorites()
    },

    methods:{
        getFavorites(){
            var url = "https://api.themoviedb.org/3/account/20727099/favorite/movies"
            //var token = JSON.parse(localStorage.getItem("userData")).token;
            var token = "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIwNjZjMGIxYzEwY2RjNjk2YTVmY2U1N2VlNTVlZTM4YyIsInN1YiI6IjY1NWMyOWM5NTM4NjZlMDExYzBhYTA1YyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.PJ7b8ufGg4WfIo-buozEIQyvlUMMQNfGajibFnTX9pA";
            var header = {
                headers:{
                    Authorization: "Bearer " + token
                }
            }
            axios.get(url, header)
            .then(response => {
                this.favorites = response.data.results

            }).catch(error => {

                console.log("Error: "+ error)

            })
        }
    },

    data(){
        return{
            favorites: [ ]
        }
    }
}

</script>