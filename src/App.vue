<script lang="ts" setup>
import AddItemDrawer from '@/components/AddItemDrawer.vue'
import { Plus, RefreshCw, Search, Send, Settings, Vault } from 'lucide-vue-next'
import { ref } from 'vue'

const isAddItemDrawerOpen = ref(false)
</script>

<template>
  <div class="h-screen flex flex-col">
    <div class="px-4 pt-2 pb-3 border-b border-gray-300 bg-white">
      <div class="size-6 mb-5 grid place-content-center text-2xs rounded-full bg-cyan-400">
        UD
      </div>
      <div class="mb-3 text-2xl font-bold">
        My vault
      </div>
      <div class="relative">
        <Search class="absolute top-2.5 left-2 size-4 text-gray-400" />
        <input class="w-full h-9 rounded-xl bg-gray-100 pl-6.5 placeholder:text-gray-400 focus-visible:outline-none" type="text" placeholder="Search">
      </div>
    </div>

    <div class="relative grow grid place-content-center bg-slate-100">
      <div>
        <div class="mb-6 text-center font-bold">
          Save and protect your data
        </div>
        <div class="mb-6 text-center text-sm">
          The vault protects more than just your <br> passwords. Store secure logins, IDs, cards <br> and notes securely here.
        </div>
        <button
          class="mx-auto h-10 flex items-center px-9 text-sm font-bold text-white rounded-full bg-blue-700"
          @click="isAddItemDrawerOpen = true"
        >
          <Plus class="mr-1.5 size-5" />
          New login
        </button>
      </div>
      <button
        class="absolute bottom-4 right-4 size-12 grid place-content-center text-white rounded-full  bg-blue-700"
        @click="isAddItemDrawerOpen = true"
      >
        <Plus class="size-8" />
      </button>
    </div>

    <div class="px-4 pt-1 flex justify-around border-t border-gray-300 text-slate-500 bg-white">
      <div class="flex flex-col items-center text-blue-700">
        <Vault class="size-7" />
        <span class="text-2xs">
          My vault
        </span>
      </div>
      <div class="flex flex-col items-center">
        <Send class="size-7" />
        <span class="text-2xs">
          Send
        </span>
      </div>
      <div class="flex flex-col items-center">
        <RefreshCw class="size-7" />
        <span class="text-2xs">Generator</span>
      </div>
      <div class="flex flex-col items-center">
        <Settings class="size-7" />
        <span class="text-2xs">Settings</span>
      </div>
    </div>

    <AddItemDrawer v-model:open="isAddItemDrawerOpen" />
  </div>
</template>
