<script>
import axios from "axios";

export default {
  data: function () {
    return {
      editMovieParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id + ".json").then((response) => {
      this.editMovieParams = response.data;
    });
  },
  methods: {
    updateMovie: function () {
      axios
        .patch("/movies/" + this.editMovieParams.id + ".json", this.editMovieParams) //this.$route.params.id
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyMovie: function () {
      axios.delete("/movies/" + this.editMovieParams.id).then((response) => {
        console.log("Success!", response.data);
        this.$router.push("/movies");
      });
    },
  },
};
</script>

<template>
  <div class="movies-edit">
    <div>
      <h1>Update Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <p>
        Title:
        <input type="text" v-model="editMovieParams.title" />
      </p>
      <p>
        Year:
        <input type="text" v-model="editMovieParams.year" />
      </p>
      <p>
        Plot:
        <input type="text" v-model="editMovieParams.plot" />
      </p>
      <p>
        Director:
        <input type="text" v-model="editMovieParams.director" />
      </p>
      <button v-on:click="updateMovie()">Save updates</button>
    </div>
    <button v-on:click="destroyMovie()">Delete movie</button>
  </div>
</template>
