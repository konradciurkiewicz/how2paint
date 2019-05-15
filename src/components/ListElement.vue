<template>
  <div class="listElement">
      <div class="box">
        <article class="media">
            <div class="media-left">
            <figure class="image ">
                <img v-bind:src="image.largeImageURL" alt="Image">
            </figure>
            </div>
            <div class="media-content">
            <div class="content">
                <p>
                <strong>John Smith</strong> <small>@johnsmith</small> <small>31m</small>
                <br>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean efficitur sit amet massa fringilla egestas. Nullam condimentum luctus turpis.
                </p>
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

</style>
