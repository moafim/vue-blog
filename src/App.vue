<template>
  <v-app>
    <!-- <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify</span>
        <span class="font-weight-light">MATERIAL DESIGN</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat href="https://github.com/vuetifyjs/vuetify/releases/latest" target="_blank">
        <span class="mr-2">Latest Release</span>
      </v-btn>
    </v-toolbar>-->
    <!-- <router-link to="/">Home</router-link>|
    <router-link to="/about">About</router-link>-->
    <v-container id="m-pad" fluid grid-list>
      <Header title="Our Blog" subtitle="Home - Blog"/>
      <v-container fluid>
        <v-layout row>
          <v-flex xs10 offset-xs1>
            <v-layout row style="margin-top: 128px; margin-bottom: 128px;">
              <v-flex xs8>
                <router-view/>
              </v-flex>
              <v-flex xs4>
                <Sidebar/>
              </v-flex>
            </v-layout>
          </v-flex>
        </v-layout>
      </v-container>
      <Footer/>
    </v-container>
  </v-app>
</template>

<script>
import axios from "axios";

import Header from "./components/Header";
import Footer from "./components/Footer";
import Sidebar from "./components/Sidebar";

export default {
  name: "App",
  components: {
    Header,
    Footer,
    Sidebar
  },
  data: () => ({
    erros: [],
    postBody: {
      email: "admin@vue.com",
      password: "Aa1234567"
    }
  }),
  created() {
    axios
      .post(`${this.$store.getters.url}/users/login`, {
        user: this.postBody
      })
      .then(response => {
        this.$store.commit("setToken", response.data.user.token);
      })
      .catch(e => {
        this.erros.push(e);
      });
  }
};
</script>

<style>
#m-pad {
  padding: 0;
}
</style>
