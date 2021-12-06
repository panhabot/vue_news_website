<template>
  <div class="app">
      <Header></Header>
      <Home></Home>
      <Footer></Footer>
  </div>
</template>


<script>

import Header from './components/Header.vue'
import Home from './views/Home.vue'
import Footer from './components/Footer.vue'
export default {
  components:{
    Header,
    Home,
    Footer
  }
}
</script>
<style>

</style>
