<script lang="ts" setup>
import {
  Collapsible,
  CollapsibleContent,
  CollapsibleTrigger,
} from '@/components/ui/collapsible'
import {
  Drawer,
  DrawerContent,
  DrawerHeader,
  DrawerTitle,
} from '@/components/ui/drawer'

import {
  DropdownMenu,
  DropdownMenuContent,
  DropdownMenuItem,
  DropdownMenuRadioGroup,
  DropdownMenuRadioItem,
  DropdownMenuTrigger,
} from '@/components/ui/dropdown-menu'

import { Input, PasswordInput } from '@/components/ui/input'

import {
  Select,
  SelectItem,
} from '@/components/ui/select'

import { Switch } from '@/components/ui/switch'

import { Textarea } from '@/components/ui/textarea'

import {
  ChevronRight,
  CircleCheckBig,
  CircleHelp,
  RefreshCw,
  Settings,
} from 'lucide-vue-next'

import { ref } from 'vue'

import { Button } from './ui/button'

const isOpen = defineModel('open')

const itemType = ref('login')
const itemName = ref('')
const username = ref('')
const password = ref('')

const URI_MATCH_DETECTION = {
  DEFAULT: { label: 'Default', value: 'default' },
  BASE_DOMAIN: { label: 'Base domain', value: 'base_domain' },
  HOST: { label: 'Host', value: 'host' },
  STARTS_WITH: { label: 'Starts with', value: 'starts_with' },
  EXACT: { label: 'Exact', value: 'exact' },
  REGULAR_EXPRESSION: { label: 'Regular expression', value: 'regular_expression' },
  NEVER: { label: 'Never', value: 'never' },
} as const

const emptyUri = {
  uri: '',
  matchDetection: URI_MATCH_DETECTION.DEFAULT.value,
}

const uris = ref<{
  uri: string
  matchDetection: typeof URI_MATCH_DETECTION[keyof typeof URI_MATCH_DETECTION]['value']
}[]>([{ ...emptyUri }])

function addUri() {
  uris.value.push({ ...emptyUri })
}

function removeUri(index: number) {
  uris.value.splice(index, 1)
}

const folder = ref('no_folder')
const owner = ref('pupukaka@gmail.ru')
const notes = ref('')
</script>

<template>
  <Drawer v-model:open="isOpen">
    <DrawerContent>
      <DrawerHeader>
        <template #start>
          <button class="text-blue-700">
            Cancel
          </button>
        </template>
        <template #center>
          <span class="font-bold">Add item</span>
        </template>
        <template #end>
          <button class="text-blue-700">
            Save
          </button>
        </template>
      </DrawerHeader>
      <div class="p-4 flex flex-col gap-4 overflow-y-scroll h-[calc(100dvh-5.5rem)]">
        <span class="text-xs text-slate-500">ITEM INFORMATION</span>
        <Select v-model="itemType" label="Type">
          <SelectItem value="login">
            Login
          </SelectItem>
          <SelectItem value="card">
            Card
          </SelectItem>
          <SelectItem value="identity">
            Identity
          </SelectItem>
          <SelectItem value="Secure note">
            Secure note
          </SelectItem>
        </Select>

        <Input v-model="itemName" label="Name" />
        <Input v-model="username" label="Username">
          <RefreshCw />
        </Input>
        <PasswordInput v-model="password" label="Password">
          <CircleCheckBig />
          <RefreshCw />
        </PasswordInput>

        <span class="text-xs text-slate-500">URIS</span>
        <Input v-for="(uri, i) in uris" :key="i" v-model="uri.uri" label="URI">
          <DropdownMenu>
            <DropdownMenuTrigger>
              <Settings />
            </DropdownMenuTrigger>
            <DropdownMenuContent align="end" class="text-base">
              <Collapsible v-slot="{ open: isCollapsibleOpen }">
                <CollapsibleTrigger class="w-full">
                  <DropdownMenuItem disabled class="relative pl-8 opacity-100 border-b">
                    <ChevronRight
                      class="absolute left-1.5 size-5" :class="[{ 'rotate-90': isCollapsibleOpen }]"
                    />
                    Match detection
                  </DropdownMenuItem>
                </CollapsibleTrigger>
                <CollapsibleContent>
                  <DropdownMenuRadioGroup v-model="uri.matchDetection">
                    <DropdownMenuRadioItem
                      v-for="matchDetection in Object.values(URI_MATCH_DETECTION)"
                      :key="matchDetection.value"
                      :value="matchDetection.value"
                      class="border-b"
                    >
                      {{ matchDetection.label }}
                    </DropdownMenuRadioItem>
                  </DropdownMenuRadioGroup>
                </CollapsibleContent>
              </Collapsible>

              <DropdownMenuItem class="pl-8 text-red-500" @click="removeUri(i)">
                Remove
              </DropdownMenuItem>
            </DropdownMenuContent>
          </DropdownMenu>
        </Input>

        <Button variant="outline" @click="addUri()">
          New URI
        </Button>

        <span class="text-xs text-slate-500">MISCELLANEOUS</span>
        <Select v-model="folder" label="Folder">
          <SelectItem value="no_folder">
            No folder
          </SelectItem>
        </Select>

        <div class="flex justify-between items-center">
          <label class="text-sm">Favorite</label>
          <Switch />
        </div>
        <div class="flex justify-between items-center">
          <label class="text-sm">
            Master password re-prompt
            <CircleHelp class="inline size-4 text-blue-700" />
          </label>
          <Switch />
        </div>

        <span class="text-xs text-slate-500">NOTES</span>
        <Textarea v-model="notes" />

        <span class="text-xs text-slate-500">CUSTOM FIELDS</span>
        <Button variant="outline">
          New custom field
        </Button>

        <span class="text-xs text-slate-500">OWNERSHIP</span>
        <Select v-model="owner" label="Who owns this item?">
          <SelectItem value="pupukaka@gmail.ru">
            pupukaka@gmail.ru
          </SelectItem>
        </Select>
      </div>
    </DrawerContent>
  </Drawer>
</template>
