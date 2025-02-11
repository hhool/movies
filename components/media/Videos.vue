<script setup lang="ts">
import type { Media } from '~/types'

defineProps<{
  item: Media
  tid: string
}>()
</script>

<template>
  <div flex="~ col" px4 md:px14 py4 gap6>
    <div op50>
      {{ $t('{numberOfVideos} Videos', { numberOfVideos: item.videos?.results?.length || 0 }) }}
    </div>
    <div grid="~ cols-minmax-20rem" gap4>
      <!-- how to get id -->
      <VideoCard v-for="i of item.videos?.results" :key="i.id" :item="i" :tid="Number(tid)" />
    </div>
  </div>
</template>
