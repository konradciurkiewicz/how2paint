<template>
  <div class="listElement">
      <div class="box listElement_box">
        <article class=" columns">
            <div class="column is-two-thirds">
              <figure class="image ">
                  <img v-bind:src="image.largeImageURL" class="image listImage" alt="Image" >
              </figure>
            </div>
            <div class="column is-one-third imageInfo_container">
            <div class="content imageInfo ">
                <div class="column is-12">
                  <h4 class="imageInfo_title">Trees and water</h4> 
                  <div class="mt-2">
                    <span>Category:</span> 
                    <strong>
                      <a href="#"> Watercolors</a>
                    </strong>
                  </div>
                  <div class="mt-2 mb-2"> 
                    
                    <div class="tags"> 
                      <span class="tag">One</span>
                      <span class="tag">Two</span>
                      <span class="tag">Three</span>
                      <span class="tag">Four</span>
                  
                    </div>
                  </div>
                </div>
                <div class="column is-12 pb-0 imageInfo_buttonsContainer">
                  <a class="imageInfo_btn button is-medium is-fullwidth">
                    <span class="icon">
                      <font-awesome-icon icon="pencil-alt" />   
                     </span>
                    <span class="listElement_showMore">Get sketch</span>
                  </a>
                  <a class="imageInfo_btn button is-medium is-fullwidth">
                    <span class="icon">
                        <font-awesome-icon icon="book-reader" />
                    </span>
                    <span class="listElement_showMore">Tutorial</span> 
                  </a>
                </div>
                
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
    font-size: 1.1em;
  }
  .listImage {
    max-height: 100vh;
    margin: 0 auto;
  }
  .listElement {
    margin-bottom: 1em;
  }
  .listElement_box {
    box-shadow: none !important;
  }
  .mt-2 {
    margin-top: 1em;
  }
  .mb-2 {
    margin-bottom:1em;
  }
  .imageInfo {
    display: flex;
    flex-wrap: wrap;
    height: 100%;
  }
  .imageInfo_btn {
    margin-top: 0.5em;
  }
  .imageInfo_btn:first-child {
    margin-top: auto;
  }
  .pb-0{
    padding-bottom:0;
  }
  .listElement_showMore {
    margin-right: 1em;
  }
  .imageInfo_buttonsContainer{
    display: flex !important;
    flex-direction: column !important;
  }
</style>
