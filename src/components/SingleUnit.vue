<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" justify="center">
      <v-col class="col-4">
        <v-card>
          <v-form>
            <v-text-field
              v-on:keyup="getSentiment()"
              v-model="word"
              placeholder="Type the word here"
              class="ma-3"
            />
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
</template>

<script>
import axios from "axios";

export default {
  name: "SingleUnit",
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