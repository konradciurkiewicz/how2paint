<template>
  <div class="listElement">
      <div class="box">
        <article class=" columns">
            <div class="column is-three-quarters">
              <figure class="image ">
                  <img v-bind:src="image.largeImageURL" class="image listImage" alt="Image" >
              </figure>
            </div>
            <div class="column is-one-quarters">
            <div class="content imageInfo">
                
                <strong class="imageInfo_title">John Smith</strong> 
                <small>@johnsmith</small> <small>31m</small>
                <br>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean efficitur sit amet massa fringilla egestas. Nullam condimentum luctus turpis.
                
            </div>
           
            </div>
        </article>
</div>
  </div>
</template>
<script>
  export default {
    name: 'ListElement',
    // To use props, they must be declared
    props: {
      image: Object,
      
    }
  }
</script>
<style lang="scss">
  .imageInfo_title{
    display: block;
  }
  .listImage {
    max-height: 100vh;
    margin: 0 auto;
  }
  .listElement {
    margin-bottom: 1em;
  }
</style>
