<template>
  <div class="nav-bar">
    <img src="@/assets/Vue-JS-logo.svg" alt="Vue logo" height="100" width="100">
    <h1>{{ headerTitle }}</h1>
  </div>

</template>

<script>
export default {
  name: "Header",
  props: {
    headerTitle: String
  }
}


</script>

<style scoped>
.nav-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #eeeeee;
  border-bottom: solid 5px #41b883;
  padding: 10px 40px;
  margin-bottom: 40px;
}

</style>