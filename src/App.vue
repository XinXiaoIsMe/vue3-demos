<script setup>
import { ref } from 'vue'
import DRate from './components/rate/index.vue'

const tip = ref({
  '1-3': '有待努力',
  '4-6': '很不错哦'
})
</script>

<template>
  <div class="app">
    <DRate :tip="tip" :length="6" />
  </div>
</template>

<style lang="scss">
.app {
  height: 100%;
}
</style>
