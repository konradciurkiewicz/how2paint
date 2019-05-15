<template>
  <div class="listView">
      <ListElement v-for="image in images" v-bind:key="image.id" v-bind:image="image" />
  </div>
</template>
<script>
import ListElement from '@/components/ListElement.vue'
import axios from 'axios'

export default {
    data() {
         return  {
             images: ['aaa', 'bbb'],
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
