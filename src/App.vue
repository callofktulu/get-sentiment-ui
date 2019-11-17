<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list dense>
        <v-list-item>
          <v-list-item-action>
            <v-icon>mdi-home</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>
              <router-link to="/">Home</router-link>
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item>
          <v-list-item-action>
            <v-icon>mdi-contact-mail</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <router-link to="/about">Multi word analysis</router-link>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app color="blue" dark>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>Sentiment Analyzer</v-toolbar-title>
    </v-app-bar>

    <v-content>

      <router-view/>

      
    </v-content>
    <v-footer color="blue" app>
      <span class="white--text">&copy; 2019 Tuğrul Ertürk</span>
    </v-footer>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
//import SingleUnit from './components/SingleUnit.vue';
import axios from "axios";

export default {
  name: "App",
  props: {
    source: String,
    word: String,
    sentiment: []
  },
  methods: {
    getSentiment() {
      axios
        .get("http://127.0.0.1:8000/sentiment/" + this.word)
        .then(response => (this.sentiment = response));
    }
  },
  components: {
    // HelloWorld,
    // SingleUnit,
  },
  data: () => ({
    drawer: null,
    sentiment: null
  })
};
</script>
