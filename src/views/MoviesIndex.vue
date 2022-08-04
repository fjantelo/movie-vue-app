<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
      currentMovie: {},
      titleFilter: "",
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies.json").then((response) => {
        this.movies = response.data;
        console.log("All Movies:", this.movies);
      });
    },
    filterMovies: function () {
      return this.movies.filter((movie) => {
        var lowerTitle = movie.title.toLowerCase();
        var lowerTitleFilter = this.titleFilter.toLowerCase();
        return lowerTitle.includes(lowerTitleFilter);
      });
    },
  },
};
</script>

<template>
  <div>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h3>
        <router-link :to="`/movies/${movie.id}`">{{ movie.title }}</router-link>
      </h3>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>Director: {{ movie.director }}</p>
    </div>
  </div>
</template>
