<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newMovieParams: { plot: "" },
      errors: [],
      status: "",
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      axios
        .post("/movies.json", this.newMovieParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
          this.status = error.response.status;
        });
    },
  },
};
</script>

<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <img v-if="status" :src="`https://http.dog/${status}.jpg`" width="500" alt="" />
      <ul>
        <li v-for="error in errrors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMovieParams.plot" />
        <small>{{ 140 - newMovieParams.plot.length }} chracters remaining</small>
      </div>
      <div>
        <label>Director:</label>
        <input type="text" v-model="newMovieParams.director" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
