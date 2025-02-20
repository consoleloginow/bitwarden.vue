<script setup lang="ts">
const modelValue = defineModel<string>({ required: true })

// https://css-tricks.com/the-cleanest-trick-for-autogrowing-textareas/
</script>

<template>
  <div
    class="grid after:content-[attr(data-replicated-value)_'_'] after:col-span-full after:row-span-full after:px-4 after:py-2.5 after:invisible whitespace-pre-wrap"
    :data-replicated-value="modelValue"
  >
    <textarea
      v-model="modelValue"
      class="col-span-full row-span-full w-full rounded-lg bg-white px-4 py-2.5 overflow-hidden resize-none focus-visible:outline-none"
    />
  </div>
</template>
