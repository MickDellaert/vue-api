<template>
  <div class="nav-bar">
    <img @click="reloadPage" src="@/assets/food-serving.png" alt="Vue logo">
    <h1>{{ headerTitle }}</h1>
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
  font-style: normal;
  font-size: 25px;
}

.nav-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #f3f3f3;
  border-top: solid 5px #ff4c00;
  padding: 0 30px;
  box-shadow: 0px 2px 6px 1px rgba(0, 0, 0, 0.13), 0px 10px 15px 5px rgba(0, 0, 0, 0.05);
}

img {
  width: 40px;
}

</style>