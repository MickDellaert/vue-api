<template>
  <div class="nav-bar">
    <img @click="reloadPage" src="@/assets/food-serving.png" alt="Vue logo">
    <h1 class="delish-title">{{ headerTitle }}</h1>
  </div>

</template>

<script>
export default {
  name: "Header",
  props: {
    headerTitle: String,
  },
  methods: {
    reloadPage(){
      window.location.reload()
    }
  }
}

</script>

<style scoped>

h1 {
  font-weight: 300;
  font-style: normal;
  font-size: 25px;
  float: right;
  margin-right: 40px;
}

.nav-bar {
  /*display: flex;*/
  /*justify-content: space-between;*/
  /*align-items: center;*/
  background-color: white;
  border-top: solid 5px #06c167;
  /*border-top: solid 5px #ff4c00;*/

  /*padding: 0 30px;*/
  box-shadow: 0px 2px 6px 1px rgba(0, 0, 0, 0.13), 0px 10px 15px 5px rgba(0, 0, 0, 0.05);
  position: fixed;
  width: 100%;
  top: 0;
  /*left: 0;*/
  /*right: 0;*/
}

img {
  float: left;
  width: 40px;
  cursor: pointer;
  margin-top: 12px;
  margin-left: 40px;
}

</style>