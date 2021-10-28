<template>
  <ol>
    <li class="item">
      <div class="bold" @click="toggle">
        {{ items.name }}
        <span>[{{ isOpen ? '-' : '+' }}]</span>
      </div>
      <ol v-if="isOpen">
        <File
          :item="item"
          v-for="item in items.contents"
          :key="item.name"
        ></File>
      </ol>
    </li>
  </ol>
</template>

<script>
import File from './File.vue';

export default {
  name: 'Directory',

  components: {
    File,
  },

  props: {
    items: {
      type: Object,
      required: true,
    },
  },

  data: () => ({
    isOpen: false,
  }),

  methods: {
    toggle() {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>
