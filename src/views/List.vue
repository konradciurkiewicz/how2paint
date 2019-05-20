<template>
  <div class="listView">
      <section class="hero">
        <div class="hero-body">
            <div class="container">
            <h1 class="title">
                Best water color inspirations
            </h1>
            <h2 class="subtitle">
                Best of water color paintings.
            </h2>
            </div>
        </div>
        </section>
        <div class="container is-fullhd">
            <img id="fsdfsdfsdf" src="" >
            <ListElement v-for="image in images" v-bind:key="image.id" v-bind:image="image" />
        </div>
  </div>
</template>
<script>
import ListElement from '@/components/ListElement.vue'
import axios from 'axios'
import cannyEdgeDetector from "canny-edge-detector";
import Image from "image-js";

Image.load(
  "https://pixabay.com/get/55e2d4414f56a914f6da8c7dda79347f153adde2574c704c702778d39e45c15a_1280.jpg"
).then(img => {
  const grey = img.grey();
    let treshold = grey.getThreshold();

  const edge = cannyEdgeDetector(grey, {
      lowThreshold:0.7*treshold,
      highThreshold:treshold,
      gaussianBlur: 1.1
  });
    console.log(edge);

    var outImg = edge.invert();
    document.getElementById('fsdfsdfsdf').src = outImg.toDataURL();

});

export default {
    data() {
         return  {
             images: [{}],
         }
    },
    components: {
        ListElement
    },
    methods: {
        drawList(){
        }
    },
    created() {
   
        axios.get('https://pixabay.com/api/?key=3105374-eecb5450ec501c01283fdc969&q=oil+sea')
        .then( response => {

            this.images = response.data.hits;
            console.log(this.images);

        })
        .catch( error => {
            console.log(error);

        })
        .finally(function () {
            // always executed
        });
    }
}
</script>
<style lang="scss">

</style>
