<script setup lang="ts">
import type { LineHeight } from '~/composables/settings'

const userSettings = useUserSettings()

const sizes: LineHeight[] = ['narrow', 'normal', 'wide']

const currentSize = computed(() => userSettings.value.lineHeight || sizes[1])

function setLineHeight(size: string) {
  userSettings.value.lineHeight = size
}
</script>

<template>
  <section space-y-2>
    <h2 id="interface-lh" font-medium>
      {{ $t('settings.interface.line_height') }}
    </h2>
    <div flex="~ gap4 wrap" p2 role="group" aria-labelledby="interface-lh">
      <button
        v-for="size in sizes"
        :key="size"
        type="button"
        btn-text flex-1 flex="~ gap-1 center" p4 border="~ base rounded" bg-base ws-nowrap
        :aria-pressed="currentSize === size ? 'true' : 'false'"
        :class="currentSize === size ? 'pointer-events-none' : 'filter-saturate-0'"
        @click="setLineHeight(size)"
      >
        {{ $t(`settings.interface.${size}`) }}
      </button>
    </div>
  </section>
</template>
