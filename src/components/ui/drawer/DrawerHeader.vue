<script lang="ts" setup>
import type { HtmlHTMLAttributes } from 'vue'
import { cn } from '@/lib/utils'

const props = defineProps<{
  class?: HtmlHTMLAttributes['class']
}>()
</script>

<template>
  <div :class="cn('grid grid-cols-3 justify-between p-4 rounded-t-[10px] border-b border-gray-300 bg-white', props.class)">
    <div class="justify-self-start">
      <slot name="start" />
    </div>
    <div class="justify-self-center">
      <slot name="center" />
    </div>
    <div class="justify-self-end">
      <slot name="end" />
    </div>
  </div>
</template>
