<template>
  <Header header-title="Delish Delights"></Header>
  <HelloWorld/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Header from "./components/Header";

export default {
  name: 'App',
  components: {
    Header,
    HelloWorld
  }
}
</script>

<style>
html {
  height: 100%;
}

body {
  height: 100%;
  margin: 0;
  background-image: linear-gradient(rgba(255,255,255,0.55), rgba(255,255,255,0.55)), url("./assets/1537710913.jpg");
  background-position:  center center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
}

@media (max-width: 1073px) {
  body {
    background-position:  center top;
  }
}

@media (max-width: 815px) {
  body {
    background-position:  center top;
  }
}

@media (max-width: 555px) {
  body {
    background-position:  center top;
  }
}

#app {
@import url('https://fonts.googleapis.com/css2?family=ABeeZee:ital@0;1&display=swap');
  font-family: 'ABeeZee', sans-serif, Helvetica, Arial, sans-serif;
  font-weight: 400;
  font-style: italic;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}

</style>
