<template>
  <div id="app">
    <slider :sliderWidth="sliderWidth" 
    :sliderHeight="sliderHeight" 
    :intervalTijd="intervalTijd"></slider>
  </div>
</template>

<script>
import Slider from './components/Slider.vue'

export default {
  name: 'app',
    data() {
  return {
      sliderWidth: 720,
      sliderHeight: 430,
      intervalTijd: 5000,
    },
  },
  components: {
    Slider,
  },

}


</script>

<style>
* {
  margin: 0;
  padding: 0;
}


</style>
