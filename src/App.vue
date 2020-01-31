<template>
  <div id="app">
    <div id="nav">
      <img src="./assets/hippo.jpg" alt="Meme" />
      <router-link to="/">Home</router-link>
      <router-link to="/create">Create</router-link>
      <router-link to="/gallery">Gallery</router-link>
    </div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  height: 100px;
  padding: 15px;
  display: flex;
  align-items: center;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  vertical-align: block;
  font-size: 28px;
  padding-left: 25px;
  text-decoration: none;
}

#nav a:hover {
  text-decoration: underline;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

#nav img {
  height: 80%;
  margin-left: 10%;
}
</style>
