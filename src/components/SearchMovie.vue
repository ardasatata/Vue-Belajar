<template>
  <v-container>
    <v-layout row wrap>
      <v-flex xs12>
        <v-layout column wrap>
          <v-flex xs6>
            <v-layout row>
              <v-text-field
                v-model="searchKeyword"
                label="Search Movie"
                placeholder="Type here..."
              ></v-text-field>
              <v-btn @click="fetchResult(searchKeyword)">Search</v-btn>
            </v-layout>
          </v-flex>
        </v-layout>
        <h5>{{ this.searchKeyword }}</h5>
        <v-container v-if="loading">
          <div class="text-xs-center">
            <v-progress-circular
              indeterminate
              :size="150"
              :width="8"
              color="green"
            >
            </v-progress-circular>
          </div>
        </v-container>
        <v-container v-else-if="noData">
          <div class="text-xs-center">
            <h2>No Movie in API with {{ this.name }}</h2>
          </div>
        </v-container>

        <v-container v-else grid-list-xl>
          <v-layout wrap>
            <v-flex
              xs4
              v-for="(item, index) in movieResponse"
              :key="index"
              mb-2
            >
              <v-card>
                <v-img :src="item.Poster" aspect-ratio="1"></v-img>

                <v-card-title primary-title>
                  <div>
                    <h2>{{ item.Title }}</h2>
                    <div>Year: {{ item.Year }}</div>
                    <div>Type: {{ item.Type }}</div>
                    <div>IMDB-id: {{ item.imdbID }}</div>
                  </div>
                </v-card-title>

                <v-card-actions class="justify-center">
                  <v-btn flat color="green" @click="singleMovie(item.imdbID)"
                    >View</v-btn
                  >
                </v-card-actions>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  props: ["name"],
  data() {
    return {
      movieResponse: [],
      loading: true,
      noData: false,
      searchKeyword: ""
    };
  },
  name: "SearchMovie",
  methods: {
    fetchResult(value) {
      axios
        .get(
          "http://www.omdbapi.com/?s=" +
            value +
            "&apikey=b924f94a&page=1&type=movie&Content-Type=application/json"
        )
        .then(response => {
          console.log(response);
          if (response.data.Response === "True") {
            this.movieResponse = response.data.Search;
            this.loading = false;
            this.noData = false;
          } else {
            this.noData = true;
            this.loading = false;
          }
        })
        .catch(error => {
          console.log(error);
        });
    }
  },
  mounted() {
    this.fetchResult(this.name);
  },
  watch: {
    name(value) {
      this.fetchResult(value);
    }
  }
};
</script>

<style scoped></style>
