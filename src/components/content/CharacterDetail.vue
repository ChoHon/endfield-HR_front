<template>
  <div class="bg-white">
    <div class="flex w-full justify-center">
      <img
        :src="props.characterData?.image"
        :alt="props.characterData?.title"
        class="max-w-none flex-shrink-0"
        style="transform: scale(0.8); transform-origin: top center"
      />
    </div>

    <div></div>
  </div>
</template>

<script setup lang="ts">
interface CardData {
  id: number
  title: string
  description: string
  image: string
}

interface Props {
  characterData?: CardData | null
}

const props = withDefaults(defineProps<Props>(), {
  characterData: null,
})
</script>
