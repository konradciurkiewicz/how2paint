<template>
  <div class="generator">
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
            <div class="columns" @mouseup="stopChange()">
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
        source: 'url',
        url:
          "data:image/jpeg;base64,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",
        inputFile: {
          name: 'Select image',
        },
        dataUrl: '',
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
          image =  this.inputImage.dataUrl;
          break;
        case 'url':
          image = this.inputImage.url;
          break;
      }
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

      this.inputImage.dataUrl  = URL.createObjectURL(this.inputImage.inputFile);

      this.generateSketch();
     
    }
  },
  created() {
    this.generateSketch();
  }
};
</script>
<style lang="scss">
</style>
