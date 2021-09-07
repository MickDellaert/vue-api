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
body {
  margin: 0px;
  background-image: url("./assets/1537710913_brushed.jpg");
  background-position: center top;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
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
