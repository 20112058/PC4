<template>
    <q-card class="movie-card">
        <q-card-section>
            <q-img :src="'https://image.tmdb.org/t/p/w500'+favorite.poster_path"></q-img>
        </q-card-section>
        <q-card-section>
            <q-card-title class="text-h6 font-weight-bold">{{ favorite.original_title }}</q-card-title>
            <div>Valoración: {{ favorite.vote_average}}</div>
            <div class="text-center">
                <!--<q-btn color="primary" icon="add_shopping_cart" label="Agregar"></q-btn>-->
                <q-btn @click="quitarFavoritos" class="glossy" round color="red" icon="delete" />
            </div>
        </q-card-section>
    </q-card>
</template>


<style>
.movie-card {
    width: 300px;
    background-color: #669900;
}

.movie-card q-card-section {
    height: 100px;
    overflow: hidden;
    

}
</style>


<script>
import axios from 'axios';
export default {
    name:"FavoriteItem",
    props: {
        favorite:{
            type : Object,
            required: true

        }
    },
methods:{
        quitarFavoritos(){
            var url = "https://api.themoviedb.org/3/account/20727099/favorite";
            var data = 
                {
                media_type: "movie",
                media_id: this.favorite.id,
                favorite: false
            };
            var token = "eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIwNjZjMGIxYzEwY2RjNjk2YTVmY2U1N2VlNTVlZTM4YyIsInN1YiI6IjY1NWMyOWM5NTM4NjZlMDExYzBhYTA1YyIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.PJ7b8ufGg4WfIo-buozEIQyvlUMMQNfGajibFnTX9pA";
            var header = {
                    headers: {
                        Authorization: 'Bearer ' + token
                    }
                };


            axios.post(url, data, header)
         .then(response => {
           console.log('Favorito eliminado', response.data);
         })
         .catch(error => {
         console.error('Error al eliminar favorito', error);
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