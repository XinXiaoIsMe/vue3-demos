<script>
export default {
  name: 'DIcon'
}
</script>

<script setup>
import { defineProps, computed } from 'vue'

const props = defineProps({
  iconName: {
    required: true,
    type: String
  }
})

const useHref = computed(() => '#' + props.iconName)
</script>

<template>
  <svg
    style="width: 30px; height: 30px;"
    xmlns="http://www.w3.org/2000/svg"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    viewBox="0 0 1000 1000"
  >
    <use :xlink:href="useHref" />
  </svg>
</template>
