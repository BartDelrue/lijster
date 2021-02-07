<template>
  <div class="min-vh-100 bg-washed-green  lijster-wrapper ph5-ns pv4-ns flex flex-column">
    <div class="bg-washed-blue br3 shadow-4 overflow-hidden flex-grow-1">
      <header class="bg-near-black white pv2">
        <nav class="flex flex-wrap  mw9 center ">
          <nuxt-link class="ph2 ph4-ns pv3 hover-bg-navy white link" to="/">Home</nuxt-link>
          <nuxt-link v-if="this.$auth.loggedIn" class="ph2 white link ph4-ns pv3 hover-bg-navy ml-auto" to="" @click.native="logout">
            Logout
          </nuxt-link>
          <nuxt-link v-else  class="ph2 white link ph4-ns pv3 hover-bg-navy ml-auto" to="/login">Login</nuxt-link>
        </nav>
      </header>
      <main class=" pv5 ph2 ph4-ns mw9 center">
        <Nuxt/>
      </main>
      <footer>
      </footer>
    </div>


  </div>


</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  methods: {
    logout() {
      this.$auth.logout();
    }
  }
})
</script>

<style lang="scss">
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
  Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

.gradient-bg {
  background-image: linear-gradient(transparent, #f6fffe);
}

body .lijster-wrapper *:focus {
  outline: 2px solid black;
}
</style>
