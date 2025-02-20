<script lang="ts" setup>
import type { InputEmits, InputProps } from './Input.vue'
import { useToggle } from '@vueuse/core'
import { Eye, EyeClosed } from 'lucide-vue-next'

import Input from './Input.vue'

export type PasswordInputProps = Omit<InputProps, 'type'>
export type PasswordInputEmits = InputEmits

defineOptions({
  inheritAttrs: false,
})

const props = defineProps<PasswordInputProps>()
const emits = defineEmits<PasswordInputEmits>()

const modelValue = defineModel<string>({ required: true })

const [inputType, toggleInputType] = useToggle<'password', 'text'>('password', {
  truthyValue: 'password',
  falsyValue: 'text',
})
</script>

<template>
  <Input
    v-bind="{ ...props, ...emits }"
    v-model="modelValue"
    :type="inputType"
  >
    <button @click="toggleInputType()">
      <component :is="inputType === 'password' ? Eye : EyeClosed" />
    </button>
    <slot />
  </Input>
</template>
