<template>
  <div class="min-vh-100 lijster-wrapper white ph5-ns pv4-ns flex flex-column">
    <div class="flex-grow-1 content-wrapper">
      <header class="white shadow">
        <nav class="flex flex-wrap">
          <nuxt-link class="pr2 pl1 pr4-ns pl3-ns pv3" to="/">
            <svg
              class="v-mid pr1"
              width="2em"
              height="1em"
              version="1.1"
              viewBox="0 0 119.6 69.849"
              xmlns="http://www.w3.org/2000/svg"
            >
              <g transform="translate(167.13 -160.01)" fill="none">
                <path
                  stroke-width=".4em"
                  d="m-161.56 214.08s11.424-20.165 48.843-32.189c37.419-12.024 65.105-4.6876 65.105-4.6876"
                  stroke="rgb(253, 19, 197)"
                />
                <path
                  stroke-width=".3em"
                  d="m-166.47 190.89c-6.4023-2.8822 84.805 56.856 106.83 2.3998 6.4028-15.833 3.8126-33.373-16.217-32.935-12.285 0.26842-13.201 8.4387-16.582 16.036-3.3804 7.597-21.493 53.35-21.493 53.35"
                  stroke="rgb(42, 255, 239)"
                />
              </g>
            </svg>
            Lijster</nuxt-link
          >
          <nuxt-link
            v-if="$auth.loggedIn"
            class="ph2 ph4-ns pv3 ml-auto"
            to=""
            @click.native="logout"
          >
            Logout
          </nuxt-link>
          <nuxt-link v-else class="ph2 ph4-ns pv3 ml-auto" to="/login">
            Login
          </nuxt-link>
        </nav>
      </header>
      <main class="pv5 ph2 ph4-ns mw9 center">
        <Nuxt />
      </main>
      <footer></footer>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  methods: {
    logout() {
      this.$auth.logout()
    },
  },
})
</script>

<style lang="scss">
:root {
  --accent: rgb(253, 19, 197);
  --accent-trans: rgba(253, 19, 197, 0.2);
  --primary: rgb(42, 255, 239);
  --primary-trans: rgb(42, 255, 239, 0.2);
  --body: rgb(5, 16, 57);
}

body {
  background: radial-gradient(
      circle at -52% -47%,
      #00000021 44%,
      transparent 44%
    ),
    radial-gradient(circle at -37% -43%, #00000030 48%, transparent 48%),
    radial-gradient(circle at 93% -44%, #0000001a 52%, transparent 52%),
    radial-gradient(var(--body), var(--body));
}

header {
  font-variant: small-caps;
  font-weight: bold;

  a,
  button {
    text-decoration: none;
    transition: text-shadow 0.2s ease;
    color: inherit;
  }

  @media screen and (min-width: 30em) {
    border-top-left-radius: 1rem;
    border-bottom-right-radius: 1rem;

    :first-child::after {
      border-top-left-radius: 1rem;
    }

    :last-child::after {
      border-bottom-right-radius: 1rem;
    }
  }
}

.accent {
  color: var(--accent);
}

.primary {
  color: var(--primary);
}

.min-w-320 {
  @media screen and (min-width: 30em) {
    min-width: 320px;
  }
}

.button-reset {
  border: 0;
  background: none;
  color: inherit;
  font-weight: inherit;
}

.shadow {
  box-shadow: 0 0 1px 1px var(--accent), 0 0 16px 4px var(--accent-trans);
}

.shadow--white {
  box-shadow: 0 0 1px 1px rgba(255, 198, 240, 0.3),
    0 0 12px 4px rgba(194, 237, 254, 0.3);
}

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
  background-image: radial-gradient(
      circle at 100% 100%,
      rgba(255, 237, 237, 1) 20%,
      transparent 150%
    ),
    radial-gradient(
      circle at 0% 0%,
      rgba(255, 237, 237, 1) 20%,
      transparent 150%
    );
}

.content-wrapper {
  border-top-left-radius: 1rem;
  border-bottom-right-radius: 1rem;
}

.lijster-wrapper * {
  transition: box-shadow 0.2s ease-in-out;
}

body a,
body button {
  position: relative;

  &::after {
    content: '';
    position: absolute;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    opacity: 0;
    box-shadow: 0 0 1px 1px var(--primary), 0 0 16px 4px var(--primary-trans);
    transition: opacity 0.2s ease-in-out;
  }

  &:focus,
  &:hover {
    &::after {
      opacity: 1;
    }
  }
}

.vr-r {
  position: relative;

  &::after {
    content: '';
    position: absolute;
    width: 0;
    height: 100%;
    right: 0;
    top: 0;
    box-shadow: 0 0 1px 1px var(--primary), 0 0 16px 4px var(--primary-trans);
  }
}

.vr-l {
  position: relative;

  &::after {
    content: '';
    position: absolute;
    width: 0;
    height: 100%;
    left: 0;
    top: 0;
    box-shadow: 0 0 1px 1px var(--primary), 0 0 16px 4px var(--primary-trans);
  }
}
</style>
