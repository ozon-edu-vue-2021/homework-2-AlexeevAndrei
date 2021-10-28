<template>
  <li :class="[{ active: isActive }, item]" @click="focusElement">
    <div :class="{ bold: isFolder }" @click="toggle">
      {{ item.name }}
      <span v-show="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
    </div>

    <ol v-if="item.contents && item.contents.length" v-show="isOpen">
      <File
        v-for="(child, index) in item.contents"
        :item="child"
        :key="index"
      ></File>
    </ol>
  </li>
</template>

<script>
export default {
  name: 'File',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data: function() {
    return {
      isOpen: false,
      isActive: false,
    };
  },
  computed: {
    isFolder: function() {
      return this.item.contents && this.item.contents.length;
    },
  },
  methods: {
    toggle: function() {
      if (this.isFolder) {
        this.isOpen = !this.isOpen;
      }
    },
    focusElement() {
      if (!this.isFolder) {
        this.isActive = !this.isActive;
      }
    },
  },
};
</script>

<style scoped>
.active {
  background-color: lightgray;
}
</style>
