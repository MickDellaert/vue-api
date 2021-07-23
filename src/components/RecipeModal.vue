<template>
  <div class="backdrop">
    <div class="modal">
      <h1>Modal title</h1>
      <div v-for="recipe in recipeResults" :key="recipe">
        <p> {{ recipe[0].strInstructions }}</p>
        <p>recipe</p>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: "RecipeModal",
  props: ["recipe"]
}
</script>

<style scoped>
  .modal {
    width: 400px;
    padding: 20px;
    margin: 100px auto;
    background: white;
    border-radius: 10px;
  }

  .backdrop {
    top: 0;
    position: fixed;
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    height: 100%;
  }
</style>