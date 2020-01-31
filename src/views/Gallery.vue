<template>
  <div class="gallery">
    <div v-for="meme in memes">
      <div class="meme">
        <img :src="meme.memeUrl" alt="../assets/hippo.jpg" />
        <h2 class="top">{{ meme.topText }}</h2>
        <h2 class="bottom">{{ meme.bottomText }}</h2>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import "../meme.css";
</style>

<script>
const axios = require("axios");
export default {
  data: function() {
    return {
      memes: [],
      meme: {}
    };
  },
  created: function() {
    axios
      .get("/api/memes")
      // .get("https://rocky-spire-54064.herokuapp.com/api/memes")
      .then(response => {
        this.memes = response.data;
        console.log(this.memes);
      })
      .catch(error => {
        console.log(this.error);
      });
  },
  methods: {},
  computed: {}
};
</script>