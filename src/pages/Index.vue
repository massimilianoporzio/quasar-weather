<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
      <q-input v-model="search"
               placeholder="Search"
               dark
               borderless
               >
        <template v-slot:before>
          <q-icon
            @click="getLocation"
            name="my_location" />
        </template>



        <template v-slot:append>
          <q-btn round dense flat icon="search" />
        </template>
      </q-input>
    </div>
    <template v-if="weatherData">
      <div class="col text-white text-center">
        <div class="text-h4 text-weight light">
          Cuneo
        </div>
        <div class="text-h6 text-weight-light">
          Snow
        </div>
        <div class="text-h1 text-weight-thin q-my-lg relative-position">
          <span>8</span>
          <span class="text-h4 relative-position degree">&deg;</span>
        </div>
      </div>
      <div class="col text-center">
        <img src="https://www.fillmurray.com/100/100"
             alt="">
      </div>
    </template>
    <template v-else>
      <div class="col column text-center text-white">
        <div class="col text-h2 text-weight-thin">
          Quasar<br>Weather
        </div>
        <q-btn class="col" flat>
          <q-icon
            @click="getLocation"
            left size="3em" name="my_location" />
          <div>Find my location</div>
        </q-btn>
      </div>
    </template>

    <div class="col skyline"></div>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
const name = 'PageIndex'
const search = ref('')
const weatherData = ref(null)
const lat = ref(0)
const lon = ref(0)

const getLocation = () => {
  navigator.geolocation.getCurrentPosition((pos)=>{
    console.log(pos.coords.latitude)
    lat.value = pos.coords.latitude
    lon.value=pos.coords.longitude
  })
}
</script>

<style lang="sass">
 .q-page
   background: linear-gradient(to bottom, #136a8a, #267871)
 .degree
   top: -44px
 .skyline
   flex: 0 0 100px
   background: url(../statics/skyline.png)
   background-size: contain
   background-position: center bottom
</style>
