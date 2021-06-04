<template>
  <div class="box">
    <div @mousedown="mousedown" @click="click">
      <slot></slot>
    </div>
    <!-- panel -->
    <div v-show="panelState.matches('open')" @mousedown="isToFocus = true">
      <slot name="panel"></slot>
    </div>
    <!-- invisible input -->
    <div class="invisible-input-box">
      <input
        type="text"
        readonly
        ref="input"
        @blur="blur"
        @focus="panelToggle('FOCUS')"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { createMachine } from 'xstate';
import { useMachine } from '@xstate/vue';

export default defineComponent({
  name: 'DropdownPanel',
  setup() {
    const panelMachine = createMachine({
      id: `panel`,
      initial: `close`,
      states: {
        close: {
          on: { FOCUS: `open` },
        },
        open: {
          on: { BLUR: `close` },
        },
      },
    });
    const { state: panelState, send: panelToggle } = useMachine(panelMachine);
    return {
      isToOpen: true,
      isToFocus: false,
      panelState,
      panelToggle,
    };
  },
  methods: {
    mousedown() {
      this.isToOpen = this.panelState.matches(`close`);
    },
    blur() {
      if (this.isToFocus) {
        (<HTMLInputElement>this.$refs.input).focus();
        this.isToFocus = false;
      } else {
        this.panelToggle('BLUR');
      }
    },
    click() {
      if (this.isToOpen) {
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
