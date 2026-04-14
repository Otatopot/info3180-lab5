<script setup>
    import { ref, onMounted } from "vue";
    let movies = ref([]);

    onMounted(() => {
        const fetchMovies = () => {

            fetch("/api/v1/movies", {
            method: 'GET'
            })
            .then(function (response) {
            return response.json();
            })
            .then(function (data) {
            console.log(data);
            movies.value = data.movies;
            })
            .catch(function (error) {
            console.log(error);
            });
    }

    fetchMovies(); 
});
</script>
<template>
    <div class="container my-3" style="width: 600px;">
        <h1 class="mb-3">Movies</h1>
        <div v-for="movie in movies" :key="movie.id" class="card mb-3 shadow-sm" style="max-width: 100%;">
            <div class="row g-0">
            
                <div class="col-md-4">
                    <img 
                        :src="movie.poster" 
                        class="card-img" 
                        :alt="movie.title"
                    />
                </div>
            
                <!-- Column 2: The Text (Right side) -->
                <div class="col-md-4">
                    <div class="card-body" style="width: 400px;">
                        <h5 class="card-title">{{ movie.title }}</h5>
                        <p class="card-text text-muted">{{ movie.description }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


