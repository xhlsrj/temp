<template>
  <div class="box">
    <div @mousedown="mousedown" @click="click">
      <slot></slot>
    </div>
    <!-- panel -->
    <div v-show="isShowPanel">
      <slot name="panel"></slot>
    </div>
    <!-- invisible input -->
    <div class="invisible-input-box">
      <input type="text" readonly="readonly" ref="input" @blur="blur" />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'DropdownBox',
  setup() {
    return {
      isToOpen: true,
    };
  },
  data() {
    return {
      isShowPanel: false,
    };
  },
  methods: {
    mousedown() {
      this.isToOpen = !this.isShowPanel;
    },
    blur() {
      this.isShowPanel = false;
    },
    click() {
      if (this.isToOpen) {
        this.isShowPanel = true;
        (<HTMLInputElement>this.$refs.input).focus();
      }
    },
  },
});
</script>

<style scoped>
.box {
  height: 100%;
}
.invisible-input-box {
  width: 0;
  height: 0;
  overflow: hidden;
}
</style>
