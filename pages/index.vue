<template>
  <div class="container">
    <div v-if="!$auth.loggedIn">
      <h1 class="f-headline">Lijster</h1>
    </div>
    <div v-else>
      <h1 class="f-headline-ns">Welkom terug</h1>
      <h2 class="f1-ns mb4">Jouw lijstjes</h2>
      <ul class="list pa0 flex flex-wrap">
        <li
          v-for="(l, index) in lists"
          :key="'l' + index"
          class="pa3 w-33-l w-auto-m flex-grow-1 w-100 min-w-320"
        >
          <div
            class="pb4 bb h5 dark-gray gradient-bg pa4 relative shadow--white"
          >
            <h3 class="f3 mb3 mt0 small-caps">
              {{ l.name }}
            </h3>
            <ul class="list pl2">
              <li
                v-for="(i, iindex) in l.items"
                :key="'l' + index + 'i' + iindex"
                class="mb3"
              >
                <strong>{{ i.name }}</strong>
                <p v-if="i.description">{{ i.description }}</p>
              </li>
            </ul>

            <nuxt-link
              :to="{ name: 'list-id', params: { id: l._id } }"
              class="
                top-0
                pr3
                f6
                tr
                bottom-0
                left-0
                right-0
                absolute
                link
                b
                near-black
              "
            >
              <span class="absolute bottom-0 left-0 right-0 mb2 mr3">
                bekijk deze lijst
              </span>
            </nuxt-link>
          </div>
        </li>
      </ul>
      <h3 class="f3 mb3">Maak een nieuwe lijst</h3>
      <form
        autocomplete="off"
        class="flex items-end flex-wrap w-25-l w-50-m pl2"
        @submit.prevent="addList"
      >
        <div class="flex flex-column mr3">
          <label for="name" class="mb1">Naam</label>
          <input
            id="name"
            v-model="newList.name"
            required
            class="b--near-black h2"
            type="text"
          />
        </div>
        <button
          class="
            h2
            mt3
            f6
            bg-dark-green
            hover-bg-green
            white
            b
            ba
            b--green
            shadow-1
            bw1
            ph3
            pv2
          "
          type="submit"
        >
          Verstuur
        </button>
      </form>
      <h2 class="f1 mb4 mt6">Lijstjes die je volgt</h2>
      <p>Je volgt nog geen andere lijstjes</p>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Context } from '@nuxt/types'

export default Vue.extend({
  auth: false,
  async asyncData({ $axios, $auth }: Context): Promise<void | object> {
    let lists = []
    if ($auth.loggedIn) {
      try {
        lists = await $axios.$get('/lists/all')
      } catch (e) {
        console.error(e)
      }
    }
    return { lists }
  },
  data() {
    return {
      lists: [],
      newList: {} as { name?: string },
    }
  },
  methods: {
    async fetchLists() {
      this.lists = await this.$axios.$get('/lists/all')
    },
    async addList({ target }: { target: HTMLFormElement }) {
      await this.$axios.$post('/lists/add', this.newList)
      this.lists = await this.$axios.$get('/lists/all')
      this.newList = {}
      target.reset()
    },
  },
})
</script>

<style></style>
