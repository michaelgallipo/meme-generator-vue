<template>
  <div class="edit">
    <form class="meme-form">
      <input v-model="meme.topText" ref="topText" placeholder="top text" />

      <input v-model="meme.bottomText" ref="bottomText" placeholder="bottom text" />

      <button v-on:click="save">Save</button>
    </form>

    <MemeImage v-bind:meme="{...meme}" />
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
      memeInfo: {
        memeUrl: "no meme received via props",
        topText: "no meme info available"
      }
    };
  },
  methods: {
    // updateText() {
    //   this.$emit("input", {
    //     topText: +this.$refs.topText.value,
    //     bottomText: +this.$refs.bottomText.value
    //   });
    // console.log(this.$refs.topText.value, this.meme);
    // },
    save: function() {
      const params = {
        memeUrl: this.meme.memeUrl,
        topText: this.meme.topText,
        bottomText: this.meme.bottomText
      };
      console.log(this.meme._id, params);
      axios
        .patch("/api/memes/" + this.meme._id, params)
        .then(response => {
          if (response.status === 200) {
            window.alert("Meme saved to database");
          }
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>