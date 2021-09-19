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
  background-image: linear-gradient(rgba(255,255,255,0.70), rgba(255,255,255,0.70)), url("./assets/delish-bg.jpg");
  background-position:  center center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
}

/*@media (max-width: 1073px) {*/
/*  body {*/
/*    background-position:  center top;*/
/*  }*/
/*}*/

/*@media (max-width: 815px) {*/
/*  body {*/
/*    background-position:  center top;*/
/*  }*/
/*}*/

/*@media (max-width: 555px) {*/
/*  body {*/
/*    background-position:  center top;*/
/*  }*/
/*}*/

#app {
@import url('https://fonts.googleapis.com/css2?family=ABeeZee:ital@0;1&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Raleway:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');
  font-family: 'Raleway', sans-serif, Helvetica, Arial, sans-serif;
  font-weight: 400;
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
}

</style>
