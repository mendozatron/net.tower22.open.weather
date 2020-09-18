<template>
  <q-page class="flex column">
    <div class="col q-pt-lg q-px-md">
      <q-input 
        v-model="text" 
        placeholder="Search" 
        borderless
        dark>
        
        <template v-slot:before>
          <q-icon 
          @click="getLocation"
          name="my_location" />
        </template>

        <template v-slot:append>
          <q-btn 
          round dense flat icon="search" />
        </template>
      </q-input>
    </div>
    <template v-if="weatherData">
      <div class="col text-white text-center">
        <div class="text-h4 text-weight-light">
          Huntington Beach
        </div>
        <div class="text-h6 text-weight-light">
          Sunny
        </div>
        <div class="text-h1 text-weight-thin q-my-lg
          relative-position">
          <span>72</span>
          <span class="degree text-h4 relative-position">&deg</span>
        </div>
      </div>
      <div class="col text-center center">
        <img src="https://www.fillmurray.com/100/100" alt="bill">
      </div>
    </template>
    <template v-else>
      <div class="col text-center text-white">
        <div class="co text-h2 text-weight-thin">
          Quasar<br>Weather
        </div>
        <q-btn 
        @click="getLocation"
        class="col" flat>
        <q-icon
          left size="3em" name="my_location" />
          <div>Find My Location</div>
        </q-btn>
      </div>
    </template>
    
    <div class="col skyline"></div>
  </q-page>
</template>

<script lang="ts">
import { Todo, Meta } from "components/models";
import ExampleComponent from "components/CompositionComponent.vue";
import { defineComponent, ref } from "@vue/composition-api";

export default defineComponent({
  name: "PageIndex",
  components: { ExampleComponent },
  data() {
      return {
        search: '',
        weatherData: null,
        lat: 0,
        long: 0
      }
  },
  methods: {
    getLocation() {
      
      console.log('getLocation');
      navigator.geolocation.getCurrentPosition
      (position =>{
        console.log('position', position)
        this.lat = position.coords.latitude
        this.long = position.coords.longitude

      })
    }
    // getLocations() {
    //   async () => {
    //       console.log(await getLocation())
    //   }
    // }

  },
  
  setup() {
    // const getLocation = require('electron-get-location')
    const meta = ref<Meta>({
      totalCount: 1200,
    });
    return { meta };
  },
});
</script>


<style lang="sass" >
.q-page
  background: linear-gradient(to bottom, #085078, #85d8ce)
.degree
  top: -44px
.skyline
  flex: 0 0 300px
  background: url(../../public/skyline.png)
  background-size: contain
  background-position: bottom center
</style>
