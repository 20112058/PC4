<template>
    <q-card class="movie-card">
        <q-card-section>
            <q-img :src="'https://image.tmdb.org/t/p/w500'+movie.poster_path"></q-img>
        </q-card-section>
        <q-card-section>
            <q-card-title class="text-h6 font-weight-bold">{{ movie.original_title }}</q-card-title>
            <div>Valoración: {{ movie.vote_average}}</div>
            <div class="text-center">
                <!--<q-btn color="primary" icon="add_shopping_cart" label="Agregar"></q-btn>-->
                <q-btn @click="añadirFavoritos" class="glossy" round color="yellow" icon="star" />
            </div>
        </q-card-section>
    </q-card>
</template>


<style>
.movie-card {
    width: 300px;
}

.movie-card q-card-section {
    height: 100px;
    overflow: hidden;
}
</style>


<script>
//import {useCartStore} from 'src/stores/cart-store';
import axios from 'axios';
export default {
    name:"MovieItem",
    props: {
        movie:{
            type : Object,
            required: true

        }
    },

    methods:{
        añadirFavoritos(){
            var url = "https://api.themoviedb.org/3/account/20727099/favorite";
            var data = 
                {
                media_type: "movie",
                media_id: this.movie.id,
                favorite: true
            };
            var token = "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIwNjZjMGIxYzEwY2RjNjk2YTVmY2U1N2VlNTVlZTM4YyIsInN1YiI6IjY1NWMyOWM5NTM4NjZlMDExYzBhYTA1YyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.PJ7b8ufGg4WfIo-buozEIQyvlUMMQNfGajibFnTX9pA";
            var header = {
                    headers: {
                        Authorization: 'Bearer ' + token
                    }
                };


            axios.post(url, data, header)
         .then(response => {
           console.log('Favorito añadido', response.data);
         })
         .catch(error => {
         console.error('Error al añadir favorito', error);
        });
        location.reload();
        }
    }

//     methods:{
//         addToCart() {
//             const store = useCartStore()
//             store.addToCart(this.producto)

//         }
//     },
}
</script>