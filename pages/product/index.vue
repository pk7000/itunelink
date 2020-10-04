<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col />
      <v-col>
        <v-img
          src="https://www.fifthquadrant.com.au/hs-fs/hubfs/CX_Spotlight_Img/INTEGRATIONS-iTunes.png?width=500&height=250&name=INTEGRATIONS-iTunes.png"
          class="img-fluid mx-auto "
        />
      </v-col>
      <v-col />
    </v-row>
    <v-row justify="center" align="center">
      <v-col />
      <v-col>
        <br>
        <br>
        <v-row justify="center" align="center">
          <v-text-field
            v-model="keyword"
            background-color="red lighten-3"
            hide-details
            label="Filled"
            filled
            rounded
            dense
            single-line
            type=" text"
            placeholder="Enter your song name please"
          />
          <v-btn
            color="red lighten-2"
            filled
            rounded
            v-bind="attrs"
            v-on="on"
            @click="searchData"
          >
            <v-icon>mdi-magnify</v-icon>
          </v-btn>
        </v-row>
        <v-row justify="center" align="center" />
      </v-col>
      <v-col />
    </v-row>
    <v-row>
      <v-col v-for="data in resultData" :key="data.trackId" justify="center" align="center">
        <v-card
          :title="data.title"
          hide-details
          label="Filled"
          filled
          rounded
          dense
          single-line
        >
          <v-card-text>
            {{ data.trackName }}
          </v-card-text>
          <nuxt-link :to="{ name: 'product-id', params: { id: data } }">
            <v-img
              :src="data.artworkUrl100"
              max-height="100"
              max-width="100"
            />
          </nuxt-link>
          <v-card-text>
            {{ data.artistName }}
          </v-card-text>
          <audio controls>
            <source :src="data.previewUrl" type="audio/mpeg">
          </audio>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      resultData: null,
      keyword: ''
    }
  },
  methods: {
    searchData () {
      axios
        .get(
          'https://itunes.apple.com/search?term=' + this.keyword + '&limit=30'
        )
        .then((response) => {
          this.resultData = response.data.results
        })
    }
  }
}
</script>

<style>
.theme--dark.v-application {
  background-image: url('https://cdn.dribbble.com/users/3228050/screenshots/7970397/fnatic_fanzine_artwork_lowowakita.jpg');
  background-attachment: fixed;
  background-position: 100% 100%;
  background-repeat: no-repeat;
  background-size: cover;
}
.theme--dark.v-card {
  background-color: #FFAB91;
  filter: opacity(95%);
  background-attachment: fixed;
  background-position: 100% 100%;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
