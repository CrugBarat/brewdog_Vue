<template lang="html">
  <div class="ingredients">
    <div class="beer-name">
    <p class="heading">{{this.beerIngredients.name}}</p>
    </div>
    <div class="beer-abv">
    <p class="heading">ABV {{this.beerIngredients.abv}}%</p>
    </div>
    <div class="grid-list-container">
      <div class="grid-container">
        <div class="grid">
          <div v-for="(value, key) in ingredients" :key="key" class="beer-list-container">
            <img class="img-ingredients" :src="ingredientsImage">
            <p class="key">{{ key | capitalize }}<p>
              <p class="ingredient" v-for="(ingredient, index) in value" :key="index">
                {{ ingredient }}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>

<script>
  import ingredients from '../assets/ingredients.png';

  export default {
    name: 'beer-ingredients',
    props: ['beerIngredients'],
    data () {
      return {
        ingredientsImage: ingredients
      }
    },
    computed: {
      ingredients() {
        const ingredientData = {};
        for (let ingredientKey in this.beerIngredients.ingredients) {
          if (typeof this.beerIngredients.ingredients[ingredientKey] === "string") {
            ingredientData[ingredientKey] = [
              this.beerIngredients.ingredients[ingredientKey]
            ];
          } else {
            let ingredientsList = this.beerIngredients.ingredients[ingredientKey]
            .map(ingredient => ingredient.name)
            .filter((ingredientName, index, array) =>
            array.indexOf(ingredientName) === index);
            ingredientData[ingredientKey] = ingredientsList;
          }
        }
        return ingredientData;
      }
    },
  }
</script>


<style lang="css" scoped>

  .grid-list-container {
    margin-left: 40px;
    margin-right: 20px;
    display: block;
    text-align: center;
  }

  .grid-container {
    display: inline-block;
  }

  .grid {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    padding: 40px;
    text-align: center;
  }

  .beer-list-container {
    border-style: solid;
    border-radius: 5%;
    flex: 1, 0, auto;
    padding: 20px;
    padding-left: 40px;
    padding-right: 40px;
    margin: 10px;
  }

  .beer-list-container:hover {
    background-color: #89cff0;
    border-radius: 10%;
  }

  .key {
    font-family: 'Veneer';
    font-size: 30px;
  }

  .ingredient {
    font-family: 'Roboto';
    font-size: 20px;
  }

  .img-ingredients {
    height: 50px;
  }

  .beer-name {
    font-family: 'Veneer';
    font-size: 50px;
    width: 100vw;
  }

  .beer-abv {
    font-family: 'Veneer';
    font-size: 30px;
    width: 100vw;
  }

  p.heading {
    padding: 0;
    margin: 0;
  }

  </style>
