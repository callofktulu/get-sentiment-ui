<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list dense>
        <v-list-item link href="/home">
          <v-list-item-action>
            <v-icon>mdi-home</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link href="/about">
          <v-list-item-action>
            <v-icon>mdi-contact-mail</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Single Word</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link>
          <v-list-item-action>
            <v-icon>mdi-contact-mail</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Text analysis</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar app color="blue" dark>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title>Sentiment Analyzer</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col class="col-4">
            <v-card>
              <v-form>
                <v-text-field v-model="word" placeholder="Type the word here" class="ma-3" />
                <v-spacer></v-spacer>
                <v-btn
                  color="success"
                  class="ma-3 justify-right"
                  v-on:click="getSentiment(word)"
                >Analyze</v-btn>
              </v-form>
            </v-card>
          </v-col>
          <v-col class="col-8">
            <v-simple-table v-if="sentiment">
              <tr>
                <th>Unit</th>
                <th>Positivity</th>
                <th>Negativity</th>
                <th>Objectivity</th>
                <th>Polarity</th>
                <th>Dictionary</th>
              </tr>
              <tr>
                <td>{{ sentiment.data.unit }}</td>
                <td>{{ sentiment.data.positivity }}</td>
                <td>{{ sentiment.data.negativity }}</td>
                <td>{{ sentiment.data.objectivity }}</td>
                <td>{{ sentiment.data.polarity }}</td>
                <td>{{ sentiment.data.dictionary }}</td>
              </tr>
            </v-simple-table>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
    <v-footer color="blue" app>
      <span class="white--text">&copy; 2019 Tuğrul Ertürk</span>
    </v-footer>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
// import HelloWorld from './components/SingleUnit';
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
