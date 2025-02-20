<script setup lang="ts">
import { ChevronDown } from 'lucide-vue-next'
import { SelectContent, SelectPortal, SelectRoot, SelectTrigger, SelectValue, SelectViewport } from 'radix-vue'

interface Props {
  label: string
}

const {
  label,
} = defineProps<Props>()

const modelValue = defineModel<string>({ required: true })
</script>

<template>
  <SelectRoot v-model="modelValue">
    <SelectTrigger
      class="flex h-17 w-full items-center justify-between rounded-lg bg-white px-4 py-2 text-sm text-start"
    >
      <div class="grow">
        <label class="block text-xs text-slate-500">{{ label }}</label>
        <SelectValue />
      </div>
      <ChevronDown class="w-4 h-4 opacity-50 shrink-0" />
    </SelectTrigger>

    <SelectPortal>
      <SelectContent
        class="relative z-50 max-h-96 min-w-64 overflow-hidden rounded-lg bg-white shadow-2xl"
        position="popper"
        align="center"
      >
        <SelectViewport class="divide-y">
          <slot />
        </SelectViewport>
      </SelectContent>
    </SelectPortal>
  </SelectRoot>
</template>
