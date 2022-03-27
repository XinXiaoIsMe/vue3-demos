<script>
export default {
  name: 'DRate'
}
</script>

<script setup>
import { defineProps, computed, ref } from 'vue'
import DIcon from '../icon/index.vue'

const props = defineProps({
  length: {
    type: Number,
    default: 5
  },
  tip: Object
})

const tips = createTips(props.tip)
const endIndex = ref(-1)
const clickIndex = ref(-1)
const tipIndex = computed(() => {
  return endIndex.value === -1
    ? clickIndex.value
    : endIndex.value
})

function createTips(tip) {
  const formatTips = (tip) => {
    const tips = {}
    for (const key in tip) {
      if (/^\d+-\d+$/.test(key)) {
        const [startIndex, endIndex] = key.split('-')
        for (let i = startIndex; i <= endIndex; i++) {
          tips[i] = tip[key]
        }
      } else if (/^\d+$/.test(key)) {
        tips[key] = tip[key]
      } else {
        tips[key] = ''
      }
    }
    return tips
  }

  const tips = typeof tip === 'object'
    ? formatTips(tip)
    : Array(props.length).fill().reduce((pre, next, index) => {
      pre[index + 1] = `${index + 1}星`
      return pre
    }, {})
  return ref(tips)
}
const doMouseOver = (id) => endIndex.value = id
const doMouseLeave = () => endIndex.value = clickIndex.value
const doClick = (id) => clickIndex.value = id
</script>

<template>
  <div class="d-rate" @mouseleave="doMouseLeave">
    <DIcon
      icon-name="star"
      :class="[
        'd-rate__icon',
        item <= endIndex ? 'is-active' : ''
      ]"
      v-for="item in length"
      :key="item"
      @mouseover="doMouseOver(item)"
      @click="doClick(item)"
    />
    <span class="d-rate__text" v-if="tip">{{ tips[tipIndex] || '' }}</span>
  </div>
</template>

<style lang="scss">
@import "./index.scss";
</style>
