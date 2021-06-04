<template>
  <div class="box">
    <input type="text" class="input" :value="value" @input="oninput" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "InputText",
  props: {
    value: {
      type: String,
      default: ``,
    },
  },
  methods: {
    // oninput({ target }: { target: HTMLInputElement }) {
    //   this.$emit(`update:value`, target.value);
    // },
    oninput(evt: Event) {
      this.$emit(`update:value`, (<HTMLInputElement>evt.target).value);
    },
  },
});
</script>

<style scoped>
.box {
  height: 100%;
}
.input {
  font-size: inherit;
  width: 100%;
  height: 100%;
  padding: 0;
  border: none;
  outline: none;
}
</style>
