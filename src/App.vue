<template>
  <div id="app">
    <LandingPage></LandingPage>
    <Footer></Footer>
  </div>
</template>

<script>
import LandingPage from './components/LandingPage'

import Footer from './components/Footer'

export default {
  name: 'App',
  components: {
    LandingPage,
    Footer
  }
}
</script>

<style lang="scss">
  @import "./assets/sass/main.scss";
</style>
