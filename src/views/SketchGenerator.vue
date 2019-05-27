<template>
  <div class="generator" @mouseup="stopChange()">
    <div class="container is-fluid">
      <div class="columns">
        <div class="column is-three-quarters">
          <div class="box hasLoader">
            <Loader v-if="showLoader"></Loader>
            <img v-bind:src="generetedSketch.src">
          </div>
        </div>

        <div class="column is-one-quarter">
          <div class="box has-text-centered">
            <p class="title">Chose image</p>
            <div class="file has-name">
              <label class="file-label">
                <input class="file-input" v-on:change="setImage" type="file" name="resume" accept="image/*">
                <span class="file-cta">
                  <span class="file-icon">
                    <i class="fas fa-upload"></i>
                  </span>
                  <span class="file-label">Choose a file…</span>
                </span>
                <span class="file-name">{{inputImage.inputFile.name}}</span>
              </label>
            </div>
            <p class="title">Settings</p>
            <div class="columns">
              <div class="column is-half">
                <p class="subtitle is-5">Level of details</p>
                <div @mousedown="startChange()">
                  <circle-slider
                    v-model="settings.gaussianBlur"
                    :side="150"
                    :min="0"
                    :max="10"
                    :step-size="1"
                    :circle-width-rel="20"
                    :progress-width-rel="10"
                    :knob-radius="10"
                    circle-color="#cecece"
                    progress-color="#F34213"
                    knob-color="#F4542A"
                  ></circle-slider>
                </div>
              </div>
              <div class="column is-half">
                <p class="subtitle is-5">Brightness</p>
                <div @mousedown="startChange()">
                  <circle-slider
                    v-model="sliderValue"
                    :side="150"
                    :min="0"
                    :max="10000"
                    :step-size="10"
                    :circle-width-rel="20"
                    :progress-width-rel="10"
                    :knob-radius="10"
                    circle-color="#cecece"
                    progress-color="#F34213"
                    knob-color="#F4542A"
                  ></circle-slider>
                </div>
              </div>
            </div>
            <div class="columns">
              <div class="column is-half">
                <p class="subtitle is-5">Min treshold</p>
                <div @mousedown="startChange()">
                  <circle-slider
                    v-model="settings.lowThreshold"
                    :side="150"
                    :min="0"
                    :max="startSettings.maxTreshold"
                    :step-size="5"
                    :circle-width-rel="20"
                    :progress-width-rel="10"
                    :knob-radius="10"
                    circle-color="#cecece"
                    progress-color="#F34213"
                    knob-color="#F4542A"
                  ></circle-slider>
                </div>
              </div>
              <div class="column is-half">
                <p class="subtitle is-5">Max treshold</p>
                <div @mousedown="startChange()">
                  <circle-slider
                    v-model="settings.highThreshold"
                    :side="150"
                    :min="0"
                    :max="startSettings.highThreshold*3"
                    :step-size="5"
                    :circle-width-rel="20"
                    :progress-width-rel="10"
                    :knob-radius="10"
                    circle-color="#cecece"
                    progress-color="#F34213"
                    knob-color="#F4542A"
                  ></circle-slider>
                </div>
              </div>
            </div>
            <div class="columns">
              <div class="column is-fullwidth">
                <a class="imageInfo_btn button is-primary is-medium is-fullwidth">
                  <span class="icon">
                    <font-awesome-icon icon="file-download"/>
                  </span>
                  <span class="listElement_showMore" @click="downloadSketch()">Download sketch</span>
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
import downloadjs from "downloadjs";
import Image from "image-js";
import Loader from "@/components/Loader.vue";
export default {
  data() {
    return {
      generetedSketch: {
        src: "",
        grey: null
      },
      inputImage: {
        source: 'file',
        url:
          "https://pixabay.com/get/5ee1d042484fad0bffd8992cc429377b1638daf8525474417d2878d39045_1280.jpg",
        inputFile: {
          name: 'Select image',
          arrayBuffer: null,
        },
      },
      startSettings: {
        lowThreshold: 80,
        highThreshold: 120,
        gaussianBlur: 2
      },
      settings: {
        lowThreshold: 80,
        highThreshold: 120,
        gaussianBlur: 2
      },
      sliderValue: 0,
      showLoader: false,
      timeLastChange: null
    };
  },
  components: {
    Loader
  },
  methods: {
    setDefaultSettings(img) {
      this.generetedSketch.grey = img.grey();
      let treshold = this.generetedSketch.grey.getThreshold();

      this.settings.lowThreshold = 0.7 * treshold;
      this.settings.highThreshold = treshold;
      this.settings.gaussianBlur = 1.1;
      this.startSettings = this.settings;
    },
    getImageFromSelectedSource(){
      var image;
      switch (this.inputImage.source) {
        case 'file':
          image =  this.inputImage.inputFile.arrayBuffer;
          break;
        case 'url':
          image = this.inputImage.url;
          break;
      }
      console.log(image)
      return image;
    },
    generateSketch() {
      Image.load(this.getImageFromSelectedSource()).then(img => {
        this.setDefaultSettings(img);

        this.drawSketch();
      });
    },
    startChange() {
      this.showLoader = true;
    },
    stopChange() {
      this.drawSketch();
      this.showLoader = false;
    },
    drawSketch() {
      const edge = cannyEdgeDetector(this.generetedSketch.grey, {
        lowThreshold: this.settings.lowThreshold,
        highThreshold: this.settings.highThreshold,
        gaussianBlur: this.settings.gaussianBlur
      });

      var outImg = edge.invert();
      this.generetedSketch.src = outImg.toDataURL();
    },
    downloadSketch() {
      downloadjs(this.generetedSketch.src, "sketch.png", "image/png");
    },
    setImage(e) {
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length) return;
      this.inputImage.inputFile = files[0];
      this.inputImage.source = 'file';
      var reader = new FileReader();
      this.inputImage.inputFile.arrayBuffer =  reader.readAsArrayBuffer(this.inputImage.inputFile);
      this.generateSketch();
    }
  },
  created() {
    // this.generateSketch();
  }
};
</script>
<style lang="scss">
</style>
