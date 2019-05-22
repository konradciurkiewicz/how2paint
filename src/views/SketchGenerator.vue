<template>
  <div class="generator">
      <circle-slider
  v-model="sliderValue"
  :side="150"
  :min="0"
  :max="10000"
  :step-size="100"
  :circle-width-rel="20"
  :progress-width-rel="10"
  :knob-radius="10"
></circle-slider>

      <!-- <img v-bind:src="generetedSketch.src" />  -->
  </div>
</template>
<script>
import axios from 'axios'
import cannyEdgeDetector from "canny-edge-detector";
import Image from "image-js";

export default {
    data() {
         return  {
             generetedSketch: {
                 src: '',
             },
             inputImage: {
                 url: 'https://pixabay.com/get/55e2d4414f56a914f6da8c7dda79347f153adde2574c704c702778d39e45c15a_1280.jpg'
             },
             sliderValue: 0,
         }
    },
    methods: {
        generateSketch(){
            Image.load(
                this.inputImage.url
            ).then(img => {
                const grey = img.grey();
                let treshold = grey.getThreshold();

                const edge = cannyEdgeDetector(grey, {
                    lowThreshold:0.7*treshold,
                    highThreshold:treshold,
                    gaussianBlur: 1.1
                });

                var outImg = edge.invert();
                this.generetedSketch.src = outImg.toDataURL();

            });
        }
    },
    created() {
        this.generateSketch();

    },

}
</script>
<style lang="scss">

</style>
