<template>
  <v-container grid-list-md>
    <v-layout row wrap>
      <v-flex md12 v-for="(articulo, index) in articulos" :key="index">
        <v-card>
          <nuxt-link :to="`/blog/${articulo.id}`">
            <v-card-title primary-title>{{ articulo.title }}</v-card-title>
          </nuxt-link>
          <v-card-text>{{ articulo.body }}</v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      articulos: []
    };
  },
  async created() {
    try {
      const resp = await axios.get(
        "https://jsonplaceholder.typicode.com/posts?_limit=10"
      );
      //console.log(resp.data);
      this.articulos = resp.data;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>