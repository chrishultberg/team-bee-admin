<template>
  <div class="app">
    <h2>🐝 Team Bee Admin</h2>

    <div class="button-row">
      <router-link
        to="/"
        class="text-button"
      >
        Index
      </router-link>
      <router-link
        to="/create"
        class="text-button"
      >
        Create
      </router-link>
      <router-link
        to="/dictionaries"
        class="text-button"
      >
        Dictionaries
      </router-link>
    </div>

    <router-view v-if="isLoaded">
    </router-view>
    <page-spinner v-else />
  </div>
</template>

<script>
import PageSpinner from '@/components/PageSpinner';

export default {
  name: 'App',

  components: {
    PageSpinner,
  },

  data() {
    return {
      isLoaded: false,
    };
  },

  async beforeCreate() {
    await this.$store.dispatch('loadPuzzles');

    let resp = await fetch('/data/dictionary.json');
    this.$store.state.dictionary = await resp.json();

    this.isLoaded = true;
  }
}
</script>

<style>
@import "./styles/base.css";
</style>

<style scoped>
.app {
  padding: var(--gutter);
}

.button-row {
  display: flex;
  gap: var(--gutter);
}
</style>
