<template>
  <v-container class="fill-height">
    <v-responsive
      class="align-centerfill-height mx-auto"
      max-width="900"
    >

      <div class="text-center">
        <h1 class="text-h2 font-weight-bold">¿Qué te apetece comer?</h1>
      </div>

      <div class="py-4" />

      <v-row>
        <v-col cols="12">
          <FormMain />
        </v-col>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script setup>
import FormMain from '@/components/FormMain.vue'
</script>
