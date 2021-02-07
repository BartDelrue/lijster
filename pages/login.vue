<template>
  <form class="flex flex-column w-25-l w-50-m" @submit.prevent="login()">
    <label class="mb1" for="name">email</label>
    <input
      id="name"
      v-model="email"
      class="mb3 b--near-black h2"
      type="text"
      autocomplete="username"
    />

    <label class="mb1" for="pw">Password</label>
    <input
      id="pw"
      v-model="password"
      class="mb3 b--near-black h2"
      type="password"
      autocomplete="current-password"
    />

    <button
      type="submit"
      class="f6 bg-dark-green hover-bg-green white b ba b--green shadow-1 bw1 ph3 pv2 mb2"
    >
      Send
    </button>
  </form>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'Login',
  auth: 'guest',
  data() {
    return {
      email: null,
      password: null,
    }
  },
  methods: {
    async login() {
      try {
        await this.$auth.loginWith('local', {
          data: { email: this.email, password: this.password },
        })
      } catch (err) {
        console.log(err)
      }
    },
  },
})
</script>

<style scoped></style>
