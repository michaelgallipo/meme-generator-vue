<template>
  <div class="home">
    <img alt="Landing Page" src="../assets/AcmeMeme.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<style scoped>
img {
  width: 75%;
}
</style>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "home",
  components: {
    HelloWorld
  }
};
</script>
