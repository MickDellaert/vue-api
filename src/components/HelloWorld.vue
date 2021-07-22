<template>
  <div class="hello">
    <img alt="food logo" src="@/assets/food-serving.png">

    <h1>{{ msg }}</h1>


  </div>

  <div id="vue-app">
    <h2>{{foodQuery}}</h2>
    <input v-model="foodQuery" placeholder="search by ingredient">
    <button @click="fetchFood">Search Food!</button>
  </div>

<!--  www.themealdb.com/api/json/v1/1/filter.php?i={{foodQuery}}-->


</template>

<script>
export default {
  name: 'HelloWorld',

  data(){
      return{
        foodQuery: "",
        msg: "Search for a recipe",
        url: "www.themealdb.com/api/json/v1/1/filter.php?i=chicken_breast",
        data: ""
      }
    },
    methods: {

      async fetchFood(){
        const response = await fetch( `https://www.themealdb.com/api/json/v1/1/filter.php?i=${this.foodQuery}`)
        console.log(await response.json())
      }
    }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

img{
  width: 100px;
  fill: #ff4c00;
}

</style>
