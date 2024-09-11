<template>
  <form>
    <v-select
      v-model="state.food"
      :items="food"
      label="Comida"
      required
      variant="solo"
    ></v-select>

    <v-combobox
      v-model="state.typeFood"
      :items="types"
      label="Tipo de comida"
      chips
      multiple
      variant="solo"
    ></v-combobox>

    <v-date-input
      v-model="state.date"
      label="¿Cuándo?"
      required
      prepend-icon=""
      prepend-inner-icon="$calendar"
      variant="solo"
    ></v-date-input>

    <v-slider
      :max="3"
      :ticks="tickLabels"
      show-ticks="always"
      step="1"
      tick-size="4"
      label="Precio"
      v-model="state.price"
    ></v-slider>

    <v-btn
      class="me-4"
      @click="submit"
    >
      Enviar
    </v-btn>

    <v-btn @click="clear">
      Limpiar
    </v-btn>
  </form>
</template>
<script setup>
  import { reactive, ref } from 'vue'
  import { useRouter } from 'vue-router'

  const router = useRouter();
  const initialState = {
    food: null,
    typeFood: null,
    price: 0,
    date: null,
  }

  const state = reactive({
    ...initialState,
  })
  
  const food = [
    'Desayuno',
    'Brunch',
    'Comida',
    'Merienda',
    'Cena',
    'Recena'
  ]

  const tickLabels = {
    0: '+10€',
    1: '+20€',
    2: '+30€',
    3: '+40€',
  }

  const types = [
    'Asturiana',
    'China',
    'Española',
    'Italiana',
    'Japonesa',
    'Mexicana',
    'Peruana',
    'Vegetariana',
    'Venezolana',
    'Marisco',
    'Pescado',
    'Carne',
    'Cocina de autor',
    'Saludable',
    'Hambuguesas',
    'Pizzas',
    'Kebab',
    'Repostería',
    'Helados',
    'Cafetería',
    'Tortitas',

  ]
  
  function clear () {
    Object.assign(state, initialState)
  }
  function formatDate (date) {
    date = new Date(date)
    return `${date.getFullYear()}-${date.getMonth() + 1}-${date.getDate()}` 
  }

  async function submit () {
    try {
      const stateFormated = {
        ...state,
        date: formatDate(state.date),
      }
      console.log(stateFormated)
      router.push(
        { path: '/restaurantsView', 
        query: stateFormated 
      });

    } catch (error) {
      console.error('Error during form submission:', error)
    }
  }


</script>

<style>
.container_bg {
  background-color: #f5f5f5;
  padding: 20px;
  border-radius: 10px;
}
.custom-input .v-input__control {
  background-color: #f5f5f5; /* Fondo gris claro para los inputs */
  color: #000000; /* Texto negro */
}

.custom-input .v-input__control input {
  color: #000000; /* Texto negro */
}

.custom-input .v-slider__label {
  color: #000000; /* Texto negro */
}
</style>