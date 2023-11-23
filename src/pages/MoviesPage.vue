<template> 
    <div class="movie-page">
        <div class="movie-list">
            <MovieList />
        </div>
        <div class="favorite-list">
            <FavoriteList />
        </div>     
    </div>
</template>
<style>
.movie-page {
    display: flex;
    justify-content: space-between;
    background-color: #99CC00;
}


.movie-list {
    width: 50%;
}

.favorite-list {
    width: 50%;
}
</style>

<script>

import MovieList
    from 'src/components/movie/MovieList.vue'

import FavoriteList
    from 'src/components/favorite/FavoriteList.vue'


export default {
    name:"MoviePage",
    components: {
        MovieList,
        FavoriteList
    }

}

</script>