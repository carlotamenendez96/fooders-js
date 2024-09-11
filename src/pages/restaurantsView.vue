<template>
<h1>Restaurants View</h1>
<div v-for="restaurant in restaurants" :key="restaurant.name">
  <v-card
    class="mx-auto"
    image="https://cdn.vuetifyjs.com/docs/images/cards/dark-beach.jpg"
    subtitle="Take a walk down the beach"
    :title="restaurant.name"
  >
    <template v-slot:actions>
      <v-btn
        append-icon="mdi-chevron-right"
        color="red-lighten-2"
        text="Book Activity"
        variant="outlined"
        block
      ></v-btn>
    </template>
  </v-card>
</div>  
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import restaurantsData from '@/restaurants.json'

const route = useRoute()
const queryParams = ref(route.query||{})
const restaurants = ref(restaurantsData)

console.log(queryParams.value)
console.log(restaurants.value)

const filters = {
  food: queryParams.value.food,
  typeFood: queryParams.value.typeFood,
  price: queryParams.value.price,
  date: queryParams.value.date,
}

const restaurantsFiltered = restaurants.value.filter(restaurant => {
  const hasFood = Array.isArray(restaurant.food) && restaurant.food.some(foodItem => filters.food.includes(foodItem))
  const hasTypeFood = Array.isArray(restaurant.typeFood) && restaurant.typeFood.some(typeFoodItem => filters.typeFood.includes(typeFoodItem))
  return hasFood && hasTypeFood
})
console.log(restaurantsFiltered)
</script>