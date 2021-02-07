<template>
  <div>
    <h1 class="f-headline">{{ list.name }}</h1>
    <div class="flex flex-wrap shadow-4 br2 ba b--washed-blue">
      <div class="w-100 w-70-l bg-white  pa4  ">
        <h2 class="mb3">Items</h2>
        <ul class="mb5">
          <li v-for="({_id, name, description}, i) in list.items" :key="'item'+i" class="mb3">
            <strong>{{ name }}</strong><br>
            <p style="white-space: pre-wrap" v-if="description">{{ description }}</p>
            <button type="button" class="f7 br-pill ba bw1 ph3 pv2 mb2 mt2" @click="removeItem(_id)">
              Delete item
            </button>
          </li>
        </ul>
        <h2 class="mb3">Voeg een item toe</h2>
        <form @submit.prevent="addItem" autocomplete="off" class="flex flex-column mw6">
          <label for="name" class="mb1">Naam</label>
          <input id="name" required v-model="item.name" class="mb3 b--near-black h2" type="text">
          <label for="description" class="mb">Omschrijving</label>
          <textarea id="description" v-model="item.description" class="mb3 b--near-black"></textarea>
          <button class="f6 bg-dark-green hover-bg-green white b ba b--green shadow-1 bw1 ph3 pv2 mb2" type="submit">Verstuur</button>
        </form>
      </div>
      <div class="w-100 w-30-l bg-white pa4 bl-l b--light-gray bt bt-0-l">
        <h2>Instellingen</h2>
        <div class="mt5">
          <form @submit.prevent="updateList" autocomplete="off" class="flex flex-column">
            <label class="mb3 b"><input type="checkbox" v-model="list.public" class="mr2">Gepubliceerd</label>
            <label for="publicUsername" class="mb1">Publieke gebruikersnaam</label>
            <input id="publicUsername" :disabled="!list.public" required v-model="list.publicUsername" class="mb3 b--near-black h2" type="text">
            <label for="publicListname" class="mb">Publieke naam van de lijst</label>
            <input id="publicListname" :disabled="!list.public" required v-model="list.publicName" class="mb3 b--near-black h2" type="text">
            <button class="f6 bg-dark-green hover-bg-green white b ba b--green shadow-1 bw1 ph3 pv2 mb2" type="submit">Verstuur</button>
          </form>
        </div>
        <div class="mt7">
          <h3>Danger zone!</h3>
          <button class="f6 br-pill ba  bw1 ph3 pv2 mb2" type="button" @click="removeList">
            Deze lijst verwijderen
          </button>
        </div>
      </div>
    </div>

  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import { Context } from '@nuxt/types';

export default Vue.extend({
  name: 'index.vue',
  data() {
    return {
      item: {} as { name?: string, description?: string },
      list: {} as { _id: string, name: string, description?: string }
    };
  },
  methods: {
    async updateList() {
      await this.$axios.$patch(`/lists/${this.list._id}`, this.list)
      this.list = await this.$axios.$get(`/lists/${this.list._id}`);
    },
    async removeList() {
      await this.$axios.$delete(`/lists/${this.list._id}`);
      this.$router.push('/');
    },
    async removeItem(id: string) {
      await this.$axios.$delete(`/lists/${this.list._id}/${id}`);
      this.list = await this.$axios.$get(`/lists/${this.list._id}`);
    },
    async addItem({target}: { target: HTMLFormElement }) {
      await this.$axios.$post(`/lists/${this.list._id}`, this.item);
      this.item = {};
      target.reset();
      this.list = await this.$axios.$get(`/lists/${this.list._id}`);
    }
  },
  async asyncData({params, $axios, redirect}: Context) {
    let list;
    try {
      list = await $axios.$get(`/lists/${params.id}`);
    } catch (e) {
      redirect('/404');
    }
    return {list};
  }
});
</script>

<style scoped>

</style>
