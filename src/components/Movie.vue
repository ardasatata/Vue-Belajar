<template>
  <v-container>
    <v-layout row wrap>
      <v-flex xs12>
        <v-card>
          <h2>{{ singleMovie.Title }}</h2>
          <div>{{ singleMovie }}</div>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>
<script>
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      singleMovie: ""
    };
  },
  mounted() {
    axios
      .get(
        "http://www.omdbapi.com/?apikey=b924f94a&i=" +
          this.id +
          "&Content-Type=application/json"
      )
      .then(response => {
        this.singleMovie = response.data;
        console.log(response.data);
      })
      .catch(error => {
        console.log(error);
      });
  }
};
</script>
<style></style>
