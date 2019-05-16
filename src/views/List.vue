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
            <ListElement v-for="image in images" v-bind:key="image.id" v-bind:image="image" />
        </div>
  </div>
</template>
<script>
import ListElement from '@/components/ListElement.vue'
import axios from 'axios'

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
   
        axios.get('https://pixabay.com/api/?key=3105374-eecb5450ec501c01283fdc969&q=water+colors')
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
