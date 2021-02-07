<template>
  <div>
    <h1 class="f-headline mb2">{{ list.publicName }}</h1>
    <p class="ttu dark-gray tracked mt4">{{ list.publicUsername }}</p>
    <div class="flex flex-wrap shadow-4 br2 ba b--washed-blue">
      <div class="w-100 bg-white pa4">
        <ul class="mb5">
          <li v-for="({_id, name, description}, i) in list.items" :key="'item'+i" class="mb3">
            <strong>{{ name }}</strong><br>
            <p style="white-space: pre-wrap" v-if="description">{{ description }}</p>
          </li>
        </ul>
      </div>
    </div>

  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Context } from '@nuxt/types';

export default Vue.extend({
  name: 'index.vue',
  auth: false,
  async asyncData({params, $axios, redirect}: Context) {
    let list;
    try {
      list = await $axios.$get(`/lists/public/${params.id}`);
    } catch (e) {
      redirect('/404');
    }
    return {list};
  }

});
</script>

<style scoped>

</style>
