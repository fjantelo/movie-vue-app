<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
      newMovieParams: {},
    };
  },
  created: function () {
    axios.get("/movies.json").then((response) => {
      console.log(response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>

<template>
  <div class="home">
    <h1>Add a movie</h1>
    <h3>Title:</h3>
    <input type="text" v-model="newMovieParams.title" />
    <h3>Year:</h3>
    <input type="text" v-model="newMovieParams.year" />
    <h3>Plot:</h3>
    <input type="text" v-model="newMovieParams.plot" />
    <h3>Director:</h3>
    <input type="text" v-model="newMovieParams.director" />
    <h1>Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>Title: {{ movie.title }}</h2>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>Director: {{ movie.director }}</p>
    </div>
  </div>
</template>

<style></style>
