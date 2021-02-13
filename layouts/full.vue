<template>
  <div class="min-vh-100 lijster-wrapper white ph5-ns pv4-ns flex flex-column">
    <div class="flex-grow-1 content-wrapper">
      <header class="white shadow">
        <nav class="flex flex-wrap">
          <button @click="toggleMenu()" :aria-expanded="menuCollapsed ? 'false': 'true'"
                  aria-controls="sidenav"
                  class="button-reset dn-l ph2 ph4-ns pv3">
            <svg class="mr2 v-mid" aria-hidden="true" height="1em" id="Layer_1" style="enable-background:new 0 0 32 32;" version="1.1" viewBox="0 0 32 32"
                 width="1em" xml:space="preserve" xmlns="http://www.w3.org/2000/svg"
                 xmlns:xlink="http://www.w3.org/1999/xlink">
              <path fill="#FFFFFF" d="M4,10h24c1.104,0,2-0.896,2-2s-0.896-2-2-2H4C2.896,6,2,6.896,2,8S2.896,10,4,10z M28,14H4c-1.104,0-2,0.896-2,2  s0.896,2,2,2h24c1.104,0,2-0.896,2-2S29.104,14,28,14z M28,22H4c-1.104,0-2,0.896-2,2s0.896,2,2,2h24c1.104,0,2-0.896,2-2  S29.104,22,28,22z"/>
            </svg>
            Menu
          </button>
          <nuxt-link class="ph2 ph4-ns pv3" to="/">Lijster</nuxt-link>

          <nuxt-link v-if="this.$auth.loggedIn" class="ph2 ph4-ns pv3 ml-auto" to="" @click.native="logout">
            Logout
          </nuxt-link>
          <nuxt-link v-else class="ph2 ph4-ns pv3 ml-auto" to="/login">
            Login
          </nuxt-link>
        </nav>
      </header>
      <div class="flex">
        <nav id="sidenav" tabindex="-1" class="vr-r mv5 ph2 ph4-ns aside"
             :class="menuCollapsed ? 'collapsed' : 'expanded'">
          <router-link to="/" class="db b pa2 link w-100 mb5 white"><span aria-hidden="true"><<&nbsp;</span>Home
          </router-link>
          <h2 class="small-caps">Jouw lijstjes</h2>
          <ul>
            <li>Lorem ipsum.</li>
            <li>Nisi, sint.</li>
            <li>Quae, voluptatem!</li>
            <li>Eum, officia?</li>
            <li>Debitis, numquam.</li>
          </ul>
          <h2 class="small-caps mt5">Lijstjes die je volgt</h2>
          <ul>
            <li>Lorem ipsum.</li>
            <li>Nisi, sint.</li>
            <li>Quae, voluptatem!</li>
            <li>Eum, officia?</li>
            <li>Debitis, numquam.</li>
          </ul>
        </nav>
        <main class="pv5 ph2 ph4-ns  w-100 overflow-hidden">
          <Nuxt/>
        </main>
      </div>
      <footer></footer>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data: function () {
    return {
      menuCollapsed: true
    }
  },
  methods: {
    logout() {
      this.$auth.logout()
    },
    toggleMenu() {
      this.menuCollapsed = !this.menuCollapsed
      const sidenav = document.getElementById('sidenav');
      if (!this.menuCollapsed && sidenav) {
        setTimeout(() => sidenav.focus())
      }
    }
  },
})
</script>

<style lang="scss">

nav.aside {
  transition: flex .2s ease-in-out, padding .2s ease-in-out, min-width .2s ease-in-out, max-width .2s ease-in-out, opacity .2s .2s ease-in-out;
  position: relative;
  visibility: initial;
  flex-basis: 20rem;
  min-width: 20rem;
  max-width: 20rem;
  opacity: 1;

  @media screen and (max-width: 60em) {
    &.collapsed {
      visibility: hidden;
      flex: 0 0 0;
      max-width: 0;
      min-width: 0;
      padding: 0;
      opacity: 0;
    }

    &.expanded {


      @media screen and (max-width: 30em) {
        + * {
          display: none;
        }

        min-width: 100%;
        max-width: 100%;
      }
    }
  }


}


</style>
