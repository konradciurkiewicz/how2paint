<template>
    <nav class="navbar is-fixed-top " role="navigation" aria-label="main navigation">
    <div class="container">
        <div class="navbar-brand ">
            <a class="navbar-item" href="#">
            <img src="img/logo-brush.png" alt="Brush Masters Logo"/>
            </a>
            <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
            </a>
        </div>

        <div id="navbarBasicExample" class="navbar-menu">
            <div class="navbar-end " style="width:100%;">
                <div class="navbar-item column col-12 navbar-search-container">
                    <!-- <input clas    s="input navbar-search" type="text" placeholder="Text input"> -->
                </div>
                <div class="navbar-item">
                    <div class="buttons navbar-buttons">
                    <a class="button is-primary">
                        <strong>Sign up</strong>
                    </a>
                    <a class="button is-light">
                        Log in
                    </a>
                    </div>
                </div>
            </div>
    
        </div>
        </div>
    </nav>
</template>

<script>

export default {

}
</script>
<style lang="scss">
 input.navbar-search {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background-color: transparent;
    border: 0;
    border-radius: 4px;
    box-shadow: none;
    box-sizing: border-box;
    color: #333;
   
    font-weight: 600;
    
    outline: none;
    position: relative;
    width: 100%;
    background-color: #efefef;
 }
 .navbar-buttons {
     margin-left: auto;
     margin-left: auto;
 }
 .navbar-search-container {
    
    padding-left: 5em !important;
    padding-right: 5em !important;
 }
 .navbar-item img {
     max-height: 2.75rem !important;
 }

</style>
