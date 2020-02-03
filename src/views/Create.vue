<template>
  <div class="create">
    <form class="meme-form">
      <input v-model="topText" placeholder="top text" />

      <input v-model="bottomText" placeholder="bottomText" />

      <button v-on:click="generate">New Meme</button>
      <button v-on:click="save">Save</button>
    </form>

    <div class="meme" :key="this.memeKey">
      <img :src="this.memeUrl" alt />
      <h2 class="top">{{ this.topText }}</h2>
      <h2 class="bottom">{{ this.bottomText }}</h2>
    </div>
  </div>
</template>

<style>
@import "../meme.css";
</style>

<script>
const axios = require("axios");
export default {
  props: ["meme"],
  components: {
    MemeImage
  },
  data: function() {
    return {
      error: "",
      memeKey: 101,
      allMemeImages: [],
      topText: "",
      bottomText: "",
      memeUrl: "http://i.imgflip.com/1bij.jpg"
    };
  },
  created: function() {
    console.log(this.memeUrl);
    fetch("https://api.imgflip.com/get_memes")
      .then(response => response.json())
      .then(response => {
        if (response.success !== true) {
          this.error = response.error_message;
          return;
        }
        this.allMemeImages = response.data.memes;
      })
      .catch(err => {
        this.error = "API ERROR";
      });
  },
  methods: {
    generate: function() {
      const randNum = Math.floor(Math.random() * this.allMemeImages.length);
      this.memeUrl = this.allMemeImages[randNum].url;
      this.memeKey = randNum;
      console.log(this.memeUrl, this.memeKey);
    },
    save: function() {
      const params = {
        memeUrl: this.memeUrl,
        topText: this.topText,
        bottomText: this.bottomText
      };
      axios
        .post("/api/memes", params)
        .then(response => {
          if (response.status === 200) {
            window.alert("Meme saved to database");
          }
        })
        .catch(error => {
          console.log(error);
        });
      console.log(params);
    }
  }
};
</script>