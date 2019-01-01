<template>
  <div class="dropdown">
    <div class="header">
      <span v-if="!open" @click="open = !open">Expand</span>
      <span v-if="open" @click="open = !open">Hide</span>
    </div>
    <slot v-if="open"></slot>
  </div>
</template>

<script>
export default {
  name: 'DropdownComponent',
  data() {
    return {
      open: true,
    };
  },
};
</script>

<style scoped>
.dropdown {
  min-width:200px;
}
.header {
  background: #aaa;
  width:100%;
}
</style>
