<template>
  <div>
    <h1 class="f-headline mb2">{{ list.publicName }}</h1>
    <p class="ttu tracked mt4 mb4">{{ list.publicUsername }}</p>
    <div class="flex flex-wrap shadow--white">
      <div class="w-100 pa4">
        <ul class="mb5">
          <li
            v-for="({ name, description }, i) in list.items"
            :key="'item' + i"
            class="mb3"
          >
            <strong>{{ name }}</strong
            ><br />
            <p v-if="description" style="white-space: pre-wrap">
              {{ description }}
            </p>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Context } from '@nuxt/types'

export default Vue.extend({
  name: 'IndexVue',
  auth: false,
  async asyncData({ params, $axios, redirect }: Context) {
    let list
    try {
      list = await $axios.$get(`/lists/public/${params.id}`)
    } catch (e) {
      redirect('/404')
    }
    return { list }
  },
})
</script>

<style scoped></style>
