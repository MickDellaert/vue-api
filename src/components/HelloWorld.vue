<template>
  <div class="hello">
    <img alt="food logo" src="@/assets/food-serving.png">
    <h1>{{ msg }}</h1>
  </div>

  <div class="search">
    <h2>{{ foodQuery }}</h2>
    <input v-model="foodQuery" placeholder="search by ingredient">
    <button @click="fetchFood">Search Food!</button>
  </div>

  <div class="results">
<!--    <h2>{{ mealResults }}</h2>-->
    <ul>
      <li v-for="meal in mealResults.meals" :key="meal.idMeal">
        <h4>{{meal.strMeal}}</h4>
        <img class="foodthumb" :src="meal.strMealThumb">
      </li>
    </ul>
    <img class="foodthumb" v-bind:src="mealImg">


  </div>

</template>

<script>
export default {
  name: 'HelloWorld',

  data() {
    return {
      foodQuery: "",
      msg: "Search for a recipe",
      mealResults: "",
    }
  },
  methods: {

    async fetchFood() {
      const response = await fetch(`https://www.themealdb.com/api/json/v1/1/filter.php?i=${this.foodQuery}`)
      const results = await response.json();
      this.mealResults = results
      console.log(results)
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

img {
  width: 100px;
}

.foodthumb {
  width: 200px;
}

.results{
  display: flex;
  justify-content: center;
}

</style>
