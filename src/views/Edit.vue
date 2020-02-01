<template>
  <div class="edit">
    <div>{{this.memeInfo}}</div>
  </div>
</template>

<style scoped>
@import "../meme.css";
</style>

<script>
export default {
  props: ["meme"],
  data: function() {
    console.log("reached meme edit", this.params, this.props);
    return {
      memeInfo: {
        memeUrl: "no meme received via props"
      }
    };
  },
  mounted: function() {
    console.log(this.props);
    if (this.meme) {
      this.memeInfo = this.meme;
    }
  }
};
</script>