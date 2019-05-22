<template>
  <div id="app">
    <header>
      <Navbar/>
    </header>
    <main>
    <router-view/>
    </main>
    <footer>
      
    </footer>
  </div>
</template>
<script>
import Navbar from '@/components/Navbar.vue'

export default {
  components: {
    Navbar
  }
}
</script>
<style lang="scss">
  @import "@/scss/layout.scss";

  #app {
    background: linear-gradient(#eeeeee, #ffffff 70vh);
  }
  header {
    margin-bottom: 65px;
  }
</style>
