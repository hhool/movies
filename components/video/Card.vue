<script setup lang="ts">
import { ref } from 'vue'
import type { Video } from '~/types'

const props = defineProps<{
  item: Video
  tid: number
}>()

// const showModal = useIframeModal()
const isEmbeddedPlayer = ref(false)

// 生成 vidsrc 专用播放链接
function getVidsrcUrl(vobject: object, tid: number) {
  const url = `https://vidsrc.net/embed/${tid}`
  return url
}

function play() {
  // 两种模式选择：
  // 模式 1: 直接在当前页面嵌入播放器
  isEmbeddedPlayer.value = true

  // 模式 2: 在模态框中打开
  // showModal(getVidsrcUrl(props.item.key))
}
</script>

<template>
  <button pb2 text-left @click="play()">
    <div
      block bg-gray4:10 p1 flex
      class="aspect-16/9"
      transition duration-400 relative
      hover="scale-102 z10"
    >
      <!-- 嵌入式播放器 -->
      <iframe
        v-if="isEmbeddedPlayer"
        :src="getVidsrcUrl(item, tid)"
        frameborder="0"
        allowfullscreen
        class="w-full h-full"
        allow="autoplay; encrypted-media"
      />

      <!-- 原封面内容 -->
      <template v-else>
        <NuxtImg
          :src="`/youtube/vi/${item.key}/maxresdefault.jpg`"
          width="400"
          height="600"
          format="webp"
          :alt="props.item.name"
          w-full h-full object-cover
        />
        <div flex w-full h-full absolute inset-0 op20 hover:op100 transition>
          <div i-ph-play ma text-3xl />
        </div>
      </template>
    </div>

    <!-- 下方文字信息 -->
    <div mt-2>
      {{ props.item.name }}
    </div>
    <div op60 text-sm>
      {{ props.item.type }}
    </div>
  </button>
</template>
