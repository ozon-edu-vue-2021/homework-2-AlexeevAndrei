<template>
  <div id="app">
    <Directory :items="tree" />
  </div>
</template>

<script>
import Directory from './components/Directory.vue';

export default {
  name: 'App',

  components: {
    Directory,
  },

  data: () => ({
    tree: {},
  }),

  mounted() {
    this.load();
  },

  methods: {
    async load() {
      const res = await fetch('./static/node_modules.json');
      const data = await res.json();
      this.tree = data;
    },
  },
};
</script>

<style>
.bold {
  font-weight: bold;
}

.item {
  cursor: pointer;
}
</style>
