<template>
    <nav class="navbar is-fixed-top" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
        <a class="navbar-item" href="#">
        How2paint
        </a>
        <a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        </a>
    </div>

    <div id="navbarBasicExample" class="navbar-menu">
        <div class="navbar-start column is-four-fifths">
            <div class="navbar-item">
                <input class="input navbar-search" type="text" placeholder="Text input">
            </div>
        </div>

        <div class="navbar-end column is-one-fifth">
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

</style>
