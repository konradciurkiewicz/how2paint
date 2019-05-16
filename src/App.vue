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
>
<style lang="scss">
  #app {
    background: #EEEEEE;
  }
</style>
