<template>
  <div id="app">
    <SignUpForm></SignUpForm>
    <Footer></Footer>
  </div>
</template>

<script>
import SignUpForm from './components/SignUpForm'
import Footer from './components/Footer'

export default {
  name: 'App',
  components: {
    SignUpForm,
    Footer
  }
}
</script>

<style lang="scss">
  @import "./assets/sass/main.scss";
</style>
