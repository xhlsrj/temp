<template>
  <div class="box">{{ text }}</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'FixText',
  props: {
    text: {
      type: String,
      default: '',
    },
  },
});
</script>

<style scoped>
.box {
  height: 100%;
  white-space: nowrap;
  display: flex;
  align-items: center;
}
</style>
