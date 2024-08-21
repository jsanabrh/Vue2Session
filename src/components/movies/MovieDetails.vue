<template>
    <section class="movie-details">

      <div class="back">
        <router-link to="/" class="botton">←</router-link>
      </div>

      <div class="container">
        <div class="poster">
          <img :src="movie?.Poster" :alt="movie?.Title">
        </div>
        
        <div class="info">
          <h2>{{ movie?.Title }}</h2>
          <p><strong>Plot:</strong><br> {{ movie?.Plot }}</p>
          <p><strong>Gener:</strong><br> {{ movie?.Genre }}</p>
          <p><strong>Actors:</strong><br> {{ movie?.Actors }}</p>
          <p><strong>Language:</strong><br> {{ movie?.Language }}</p>
          <p><strong>Year:</strong><br> {{ movie?.Year }}</p>
          <p><strong>Runtime:</strong><br> {{ movie?.Runtime }}</p>
          <router-link to="/" class="return">Atras</router-link>
        </div>
      </div>
      
    </section>
  </template>
  
  <script setup lang="ts">
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  import HTTP from '@/api/client-http';
  import type { Movie } from '@/model/movie.model';
  
  const route = useRoute();
  const movieId = route.params.id as string;
  
  const movie = ref<Movie>();
  
  onMounted(async () => {
    const response = await HTTP.get('', {
      params: {
        i: movieId
      }
    });
    movie.value = response.data;
  });
  </script>
  
  <style scoped lang="scss">
  .movie-details {
    display: flex;
    justify-content: space-evenly;
    flex-direction: column;
    padding: 20px;
    background-color: #f4f4f4;
    border-radius: 13px;
    max-width: 800px;
    margin: 2% auto;

    .back{
      .botton{
        background-color: $primary;
        border-radius: 50%;
        padding: 5px 7px;
        text-align: center;
        text-decoration: none;
        color: white;
        transition: 0.7s ease;  

        &:hover{
          background-color: #3b1577;
          transition: 0.7s ease;
        }
      }
    }

    .container{
      display: flex;
      flex-direction: row;
      align-items: center;

      .poster{
        width: 50%;
          img {
          min-width: 100%;
          height: auto;
          margin-bottom: 20px;
          border: 5px solid $primary;
          padding: 5px;
        }
      }

      .info{
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        text-align: center;
        width: 50%;

        h2 {
          margin-bottom: 20px;
          color: $primary;
        }
      
        .return{
          background-color: $primary;
          color: white;
          padding: 10px;
          text-decoration: none;
          border-radius: 15px;
          margin: 15px;
          transition: 0.7s ease;

          &:hover{
            background-color: #3b1577;
            transition: 0.7s ease;
          }
        }
      }
    }
  }

    
  
  
  </style>