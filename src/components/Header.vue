<template>
  <div class="nav-bar">
    <img src="@/assets/food-serving.png" alt="Vue logo">
    <h1>{{ headerTitle }}</h1>
  </div>

</template>

<script>
export default {
  name: "Header",
  props: {
    headerTitle: String,

  }
}


</script>

<style scoped>
.nav-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #eeeeee;
  border-bottom: solid 5px #ff4c00;
  padding: 10px 40px;
  margin-bottom: 40px;
}

img {
  width: 60px;
}

</style>