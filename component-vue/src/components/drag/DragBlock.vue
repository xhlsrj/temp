<template>
  <div class="box" @mouseup="endmove" @mouseleave="endmove">
    <div class="inner-box" @mousemove="mousemove"></div>
    <div
      class="block"
      :style="{ marginLeft: mlOffsetValue }"
      @mousedown="mousedown"
    ></div>
    <!-- <div class="block"></div> -->
  </div>
</template>

<script lang="ts">
import { ref, defineComponent } from 'vue';
import { log } from 'xstate/lib/actionTypes';

export default defineComponent({
  name: 'DragBlock',
  setup: () => {
    const count = ref(0);
    return { count };
  },
  data() {
    return {
      mlOffset: 0 as number,
      curTarget: null as EventTarget | null,
      curCursorX: 0 as number,
    };
  },
  computed: {
    mlOffsetValue(): string {
      return `${this.mlOffset}px`;
    },
  },
  methods: {
    mousedown(evt: MouseEvent): void {
      this.curTarget = evt.target;
      this.curCursorX = evt.offsetX;
    },
    endmove(): void {
      this.curTarget = null;
      this.curCursorX = 0;
    },
    mousemove(evt: MouseEvent): void {
      if (this.curTarget !== null) {
        this.mlOffset = evt.layerX - this.curCursorX;
      }
    },
  },
});
</script>

<style scoped>
.box,
.inner-box {
  width: 600px;
  height: 300px;
  border: 1px solid #000;
  /* position: relative; */
  position: absolute;
  z-index: 0;
}
.inner-box {
  top: 0;
  z-index: 1;
}
.block {
  position: absolute;
  top: 0;
  box-sizing: border-box;
  width: 100px;
  height: 100px;
  border: 10px solid;
  border-image: linear-gradient(#654ea3, #c471ed, #eaafc8) 10;
  cursor: move;
  user-select: none;
  z-index: 2;
}
</style>
