<template>
  <div class="generator">
    <div class="container is-fluid">
      
      <div class="columns">
        <div class="column is-three-quarters">
          <div class="box">
            <img v-bind:src="generetedSketch.src">
          </div>
        </div>
        <div class="column is-one-quarter">
          <div class="box has-text-centered	">
          <p class="title ">Settings</p>

            <div class="columns">
              <div class="column is-half">
                <p class="subtitle is-5">Level of details</p>
                <circle-slider
                  v-model="sliderValue"
                  :side="150"
                  :min="0"
                  :max="10000"
                  :step-size="100"
                  :circle-width-rel="20"
                  :progress-width-rel="10"
                  :knob-radius="10"
                  circle-color="#cecece"
                  progress-color="#F34213"
                  knob-color="#F4542A"                ></circle-slider>
              </div>
              <div class="column is-half">
                <p class="subtitle is-5">Brightness</p>
                <circle-slider
                  v-model="sliderValue"
                  :side="150"
                  :min="0"
                  :max="10000"
                  :step-size="100"
                  :circle-width-rel="20"
                  :progress-width-rel="10"
                  :knob-radius="10"
                  circle-color="#cecece"
                  progress-color="#F34213"
                  knob-color="#F4542A"             
                ></circle-slider>
              </div>

            </div>
            <div class="columns">
              <div class="column is-half">
                <p class="subtitle is-5">Min treshold</p>
                <circle-slider
                  v-model="sliderValue"
                  :side="150"
                  :min="0"
                  :max="10000"
                  :step-size="100"
                  :circle-width-rel="20"
                  :progress-width-rel="10"
                  :knob-radius="10"
                  circle-color="#cecece"
                  progress-color="#F34213"
                  knob-color="#F4542A"                ></circle-slider>
              </div>
              <div class="column is-half">
                <p class="subtitle is-5">Max treshold</p>
                <circle-slider
                  v-model="sliderValue"
                  :side="150"
                  :min="0"
                  :max="10000"
                  :step-size="100"
                  :circle-width-rel="20"
                  :progress-width-rel="10"
                  :knob-radius="10"
                  circle-color="#cecece"
                  progress-color="#F34213"
                  knob-color="#F4542A"             
                ></circle-slider>
              </div>

            </div>
            <div class="columns">
              <div class="column is-fullwidth">
                <a class="imageInfo_btn button is-primary is-medium is-fullwidth">
                    <span class="icon">
                      <font-awesome-icon icon="file-download" />   
                     </span>
                    <span class="listElement_showMore">Download sketch</span>
                  </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import cannyEdgeDetector from "canny-edge-detector";
import Image from "image-js";

export default {
  data() {
    return {
      generetedSketch: {
        src: ""
      },
      inputImage: {
        url:
          "https://pixabay.com/get/55e5dd444e52af14f6da8c7dda79347f153adde2574c704c70277fd29049c250_1280.jpg"
      },
      sliderValue: 0
    };
  },
  methods: {
    generateSketch() {
      Image.load(this.inputImage.url).then(img => {
        const grey = img.grey();
        let treshold = grey.getThreshold();

        const edge = cannyEdgeDetector(grey, {
          lowThreshold: 0.7 * treshold,
          highThreshold: treshold,
          gaussianBlur: 1.1
        });

        var outImg = edge.invert();
        this.generetedSketch.src = outImg.toDataURL();
      });
    }
  },
  created() {
    this.generateSketch();
  }
};
</script>
<style lang="scss">
</style>
