<template>
  <div class="gallery">
    <div v-for="meme in memes">
      <!-- <div class="meme">
        <img :src="meme.memeUrl" alt="../assets/hippo.jpg" />
        <h2 class="top">{{ meme.topText }}</h2>
        <h2 class="bottom">{{ meme.bottomText }}</h2>
      </div>-->
      <MemeImage v-bind:meme="{...meme}" />
      <router-link style="font-size: 24px" :to="{name: 'edit', params: {meme}}">Edit</router-link>
    </div>
  </div>
</template>

<style scoped>
@import "../meme.css";
</style>

<script>
import MemeImage from "@/components/MemeImage.vue";
const axios = require("axios");
export default {
  props: ["meme"],
  components: {
    MemeImage
  },
  data: function() {
    return {
      memes: [],
      meme: {}
    };
  },
  created: function() {
    axios
      .get("/api/memes")
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