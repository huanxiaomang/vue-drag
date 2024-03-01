<script setup lang='ts'>
defineProps({
  itemClass: {
    type: String,
    default: 'bg-yellow-300',
  },
})
</script>

<template>
  <div
    class="container"
    m-2 h-10 flex select-none items-center justify-center rounded-md :class="itemClass"
  >
    <slot />
  </div>
</template>

<style lang="less" scoped>

</style>
