<template>
  <div class="box">
    <div class="prefix-box">
      <FixText text="prefix" />
    </div>
    <div class="input-box">
      <InputText />
    </div>
    <div class="suffix-box">
      <FixText text="suffix" />
    </div>
  </div>
</template>

<script lang="ts">
import { ref, defineComponent } from 'vue';
import InputText from './InputText.vue';
import FixText from './FixText.vue';

export default defineComponent({
  name: 'InputFixBox',
  components: {
    InputText,
    FixText,
  },
});
</script>

<style scoped>
.box {
  height: 100%;
  display: flex;
}
.input-box {
  flex-grow: 1;
}
</style>
