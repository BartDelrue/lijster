<template>
  <div>
    <h1 class="f-headline-ns mt0 mb3">{{ list.name }}
      <button class="button-reset v-mid ml4" aria-label="delen" title="Delen" @click="share()"
              :style="{display: canShare ? 'initial' : 'none'}">
        <svg version="1.1" width=".8em" height=".8em" xmlns="http://www.w3.org/2000/svg"
             xmlns:xlink="http://www.w3.org/1999/xlink"
             x="0px" y="0px" viewBox="0 0 227.216 227.216">
          <path fill="#FFFFFF"
                d="M175.897,141.476c-13.249,0-25.11,6.044-32.98,15.518l-51.194-29.066c1.592-4.48,2.467-9.297,2.467-14.317  c0-5.019-0.875-9.836-2.467-14.316l51.19-29.073c7.869,9.477,19.732,15.523,32.982,15.523c23.634,0,42.862-19.235,42.862-42.879  C218.759,19.229,199.531,0,175.897,0C152.26,0,133.03,19.229,133.03,42.865c0,5.02,0.874,9.838,2.467,14.319L84.304,86.258  c-7.869-9.472-19.729-15.514-32.975-15.514c-23.64,0-42.873,19.229-42.873,42.866c0,23.636,19.233,42.865,42.873,42.865  c13.246,0,25.105-6.042,32.974-15.513l51.194,29.067c-1.593,4.481-2.468,9.3-2.468,14.321c0,23.636,19.23,42.865,42.867,42.865  c23.634,0,42.862-19.23,42.862-42.865C218.759,160.71,199.531,141.476,175.897,141.476z M175.897,15  c15.363,0,27.862,12.5,27.862,27.865c0,15.373-12.499,27.879-27.862,27.879c-15.366,0-27.867-12.506-27.867-27.879  C148.03,27.5,160.531,15,175.897,15z M51.33,141.476c-15.369,0-27.873-12.501-27.873-27.865c0-15.366,12.504-27.866,27.873-27.866  c15.363,0,27.861,12.5,27.861,27.866C79.191,128.975,66.692,141.476,51.33,141.476z M175.897,212.216  c-15.366,0-27.867-12.501-27.867-27.865c0-15.37,12.501-27.875,27.867-27.875c15.363,0,27.862,12.505,27.862,27.875  C203.759,199.715,191.26,212.216,175.897,212.216z"/>
        </svg>
      </button>
    </h1>
    <div class="mb5" v-if="canShare">
      <strong>Deel deze link met je vrienden: </strong>
      <span class="primary">{{ shareLink }}</span>
    </div>
    <div class="flex flex-wrap">
      <div class="w-100 w-70-l  pa4">
        <h2 class="mb3">Items</h2>
        <ul class="mb5">
          <li
            v-for="({ _id, name, description }, i) in list.items"
            :key="'item' + i"
            class="mb3"
          >
            <strong>{{ name }}</strong
            ><br/>
            <p v-if="description" style="white-space: pre-wrap">
              {{ description }}
            </p>
            <button
              type="button"
              class="f7 br-pill ba bw1 ph3 pv2 mb2 mt2"
              @click="removeItem(_id)"
            >
              Delete item
            </button>
          </li>
        </ul>
        <h2 class="mb3">Voeg een item toe</h2>
        <form
          autocomplete="off"
          class="flex flex-column mw6"
          @submit.prevent="addItem"
        >
          <label for="name" class="mb1">Naam</label>
          <input
            id="name"
            v-model="item.name"
            required
            class="mb3 b--near-black h2"
            type="text"
          />
          <label for="description" class="mb">Omschrijving</label>
          <textarea
            id="description"
            v-model="item.description"
            class="mb3 b--near-black"
          ></textarea>
          <button
            class="f6 bg-dark-green hover-bg-green white b ba b--green shadow-1 bw1 ph3 pv2 mb2"
            type="submit"
          >
            Verstuur
          </button>
        </form>
      </div>
      <div class="w-100 w-30-l  pa4 shadow--white">
        <h2>Instellingen</h2>
        <div class="mt5">
          <form
            autocomplete="off"
            class="flex flex-column"
            @submit.prevent="updateList"
          >
            <label for="listname" class="mb1">Naam</label>
            <input
              id="listname"
              v-model="list.name"
              required
              class="mb3 b--near-black h2"
              type="text"
            />
            <label class="mb3 b"
            ><input
              v-model="list.public"
              type="checkbox"
              class="mr2"
            />Gepubliceerd</label
            >
            <label for="publicUsername" class="mb1"
            >Publieke gebruikersnaam</label
            >
            <input
              id="publicUsername"
              v-model="list.publicUsername"
              :disabled="!list.public"
              required
              class="mb3 b--near-black h2"
              type="text"
            />
            <label for="publicListname" class="mb"
            >Publieke naam van de lijst</label
            >
            <input
              id="publicListname"
              v-model="list.publicName"
              :disabled="!list.public"
              required
              class="mb3 b--near-black h2"
              type="text"
            />
            <button
              class="f6 bg-dark-green hover-bg-green white b ba b--green shadow-1 bw1 ph3 pv2 mb2"
              type="submit"
            >
              Verstuur
            </button>
          </form>
        </div>
        <div class="mt5 " v-if="canShare">
          <strong>Deel deze link met je vrienden: </strong>
          <p class="accent">{{ shareLink }}</p>
        </div>
        <div class="mt7">
          <h3>Danger zone!</h3>
          <button
            class="f6  ba bw1 ph3 pv2 mb2"
            type="button"
            @click="removeList"
          >
            Deze lijst verwijderen
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Context } from '@nuxt/types'
import { List } from '../../../types/list';

export default Vue.extend({
  name: 'IndexVue',
  layout: 'full',
  async asyncData({params, $axios, redirect}: Context) {
    let list
    try {
      list = await $axios.$get(`/lists/${params.id}`)
    } catch (e) {
      redirect('/404')
    }
    return {list}
  },
  data() {
    return {
      item: {} as { name?: string; description?: string },
      list: {} as List,
    }
  },
  computed: {
    canShare(): boolean {
      return process.client && navigator.share && this.list.public
    },
    shareLink(): string {
      if (process.client) {
        return window.location.origin + '/list/public/' + this.list._id
      }
      return ''
    }
  },
  methods: {
    async updateList() {
      await this.$axios.$patch(`/lists/${this.list._id}`, this.list)
      this.list = await this.$axios.$get(`/lists/${this.list._id}`)
    },
    async removeList() {
      await this.$axios.$delete(`/lists/${this.list._id}`)
      this.$router.push('/')
    },
    async removeItem(id: string) {
      await this.$axios.$delete(`/lists/${this.list._id}/${id}`)
      this.list = await this.$axios.$get(`/lists/${this.list._id}`)
    },
    async addItem({target}: { target: HTMLFormElement }) {
      await this.$axios.$post(`/lists/${this.list._id}`, this.item)
      this.item = {}
      target.reset()
      this.list = await this.$axios.$get(`/lists/${this.list._id}`)
    },
    share() {
      if (navigator.share) {
        navigator.share({
          title: this.list.publicName,
          text: this.list.publicUsername + ' wil deze lijst met je delen.',
          url: this.$route,
        })
          .then(() => console.log('Successful share'))
          .catch((error) => console.log('Error sharing', error));
      }
    }
  },
})
</script>

<style scoped></style>
