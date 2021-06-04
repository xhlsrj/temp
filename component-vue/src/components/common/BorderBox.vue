<template>
  <div class="border-box">
    <slot></slot>
  </div>
</template>

<style scoped>
.border-box {
  height: 100%;
  box-sizing: border-box;
  border: 1px solid #000;
}
</style>
