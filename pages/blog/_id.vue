<template>
  <v-container grid-list-md>
    <v-layout row wrap>
      <v-flex md12>
        <v-card>
          <v-card-title primary-title>{{ articulo.title }}</v-card-title>

          <v-card-text>
            <p>{{ articulo.nombreAutor }}</p>
            {{ articulo.body }}
          </v-card-text>
          <v-card-actions>
            <v-btn color="info" text-color="white">
              <nuxt-link to="/blog" class="white--text">Atras</nuxt-link>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {};
  }/* ,
  async created() {
    try {
      const respAutor = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${this.$route.params.id}`
      );
      this.usuario = respAutor.data;

      const resp = await axios.get(
        `https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`
      );
      this.articulo = resp.data;
    } catch (error) {
      console.log(error);
    }
  } */,
  async asyncData({
    isDev,
    route,
    store,
    env,
    params,
    query,
    req,
    res,
    redirect,
    error
  }) {
    try {
      const resp = await axios.get(
        `https://jsonplaceholder.typicode.com/posts/${params.id}`
      );
      const articulo = resp.data;

      const respAutor = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${params.id}`
      );
      articulo.nombreAutor = respAutor.data.name;

      return {articulo};

    } catch (error) {
      console.log(error);
      return error
    }
  }
};
</script>