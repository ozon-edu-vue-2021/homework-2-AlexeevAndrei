<template>
  <ol>
    <li class="item">
      <div class="bold" @click="toggle">
        {{ items.name }}
        <span>[{{ isOpen ? '-' : '+' }}]</span>
      </div>
      <ol v-show="isOpen">
        <File
          :item="item"
          v-for="(item, index) in items.contents"
          :key="index"
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
  data: function() {
    return {
      isOpen: false,
    };
  },
  methods: {
    toggle: function() {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>
