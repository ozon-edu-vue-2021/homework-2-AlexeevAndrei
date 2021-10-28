<template>
  <li :class="[{ active: isActive }, item]" @click="focusElement">
    <div :class="{ bold: isFolder, link: isLink }" @click="toggle">
      {{ item.name }}
      <span v-if="isFolder">[{{ isOpen ? '-' : '+' }}]</span>
    </div>
    <template v-if="isOpen">
      <ol v-if="item.contents && item.contents.length">
        <File
          v-for="child in item.contents"
          :item="child"
          :key="child.name"
        ></File>
      </ol>
    </template>
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

  data: () => ({
    isOpen: false,
    isActive: false,
  }),

  computed: {
    isFolder() {
      return this.item.contents && this.item.contents.length;
    },
    isLink() {
      return this.item.type === 'link';
    },
  },

  methods: {
    toggle() {
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

.link {
  color: red;
}
</style>
