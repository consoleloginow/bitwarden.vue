<script setup lang="ts">
import { useId, useTemplateRef } from 'vue'

export interface InputProps {
  modelValue: string
  label: string
  type?: 'text' | 'password' | 'url'
}

export interface InputEmits {
  'update:modelValue': (value: string) => void
}

defineOptions({
  inheritAttrs: false,
})

const {
  label,
  type = 'text',
} = defineProps<InputProps>()

const modelValue = defineModel<string>({ required: true })

const id = useId()
const inputRef = useTemplateRef('input')
</script>

<template>
  <div class="flex h-17 w-full items-center justify-between rounded-lg bg-white text-sm">
    <div class="grow relative h-full flex items-center pl-4" @click="inputRef?.focus()">
      <input
        :id="id"
        ref="input"
        v-model="modelValue"
        :type="type"
        class="peer w-full pt-3.5 text-base scale-88 origin-left focus-visible:outline-none"
        placeholder=" "
      >
      <label
        class="absolute text-slate-500 peer-not-placeholder-shown:text-xs peer-focus:text-xs peer-not-placeholder-shown:top-4 peer-focus:top-4"
        :for="id"
      >{{ label }}</label>
    </div>
    <div v-if="$slots.default" class="pl-2 pr-4 flex gap-4 text-slate-500" @click.stop>
      <slot />
    </div>
  </div>
</template>
