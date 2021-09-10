<template>
  <div class="backdrop" @click="closeModal">

    <div class="modal">
      <div class="meal-title">
        <h1>{{ mealTitle }}</h1>
        <hr>
      </div>

      <div>
        <!--        <img class="foodthumb" :src="meal.strMealThumb">-->
      </div>

      <div class="modal-contents">
        <div class="ingredients">
          <h4>Ingredients</h4>
          <table>
            <tr v-for="it in ingredientsProp" :key="it.id">
              <td class="ingredient-name">{{ it.name }}</td>
              <td class="ingredient-measure">{{ it.measure }}</td>
            </tr>
          </table>
        </div>
        <div>
          <div class="preparation">
            <h4>Preparation</h4>
            <p>{{ preparation }}</p>
          </div>
        </div>
      </div>
    </div>

  </div>

</template>

<script>
export default {
  name: "RecipeModal",
  props: ["ingredientsProp", "mealTitle", "preparation", "meal"],

  methods: {
    closeModal() {
      this.$emit("close")
    }
  }
}
</script>

<style scoped>

h1 {
  margin-top: 0;
  text-align: left;
}

hr {
  border: 1px solid #fdded1;
}

h4 {
  color: #ff4c00;
  text-align: left;
}

p {
  text-align: left;
}

.meal-title {
  width: 100%
}

.modal-contents{
  display: flex;
}

.ingredients{
  margin-right: 50px;
}

.preparation {

}

.modal {
  font-family: Raleway;
  font-style: normal;
  font-size: 14px;
  line-height: 1.5;
  line-height: 1.5;
  padding: 20px;
  margin: 50px 50px;
  background: white;
  border-radius: 5px;
  white-space: break-spaces;
  max-height: 100%;
  overflow-y: auto;
}

.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}

table {
  border-collapse: collapse;
  line-height: 1.5;
  width: 300px;
}

td {
  font-size: 14px;
}

tr {
  border-bottom: dimgray 1px solid;
}

.ingredient-name {
  text-align: left;
}

.ingredient-measure {
  text-align: right;
}

@media (max-width: 1073px) {
  .modal {
    width: 80%;
  }
}

@media (max-width: 815px) {
  .modal {
    width: 80%;
  }
}

@media (max-width: 555px) {
  .modal {
    width: 80%;
  }
}
</style>