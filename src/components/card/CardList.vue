<script setup lang="ts">
import BaseCard from '@/components/card/BaseCard.vue'
import { ref, onMounted } from 'vue'

interface CardData {
  id: string
  title: string
  description: string
  image: string
  imgPosition: number
  imgScale: number
}

const cards = ref<CardData[]>([])

// JSON 파일에서 데이터 로드
const loadCards = async () => {
  try {
    const response = await fetch('/public/data/cards.json')
    cards.value = await response.json()
  } catch (error) {
    console.error('카드 데이터 로드 실패:', error)
  }
}

onMounted(loadCards)
</script>

<template>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
    <div v-for="card in cards" :key="card.title">
      <BaseCard>
        <template #image>
          <img
            :src="card.image"
            alt="card image"
            class="w-full h-full object-cover"
            :style="{
              objectPosition: `0% ${card.imgPosition}%`,
              transform: `scale(${card.imgScale})`,
            }"
          />
        </template>
        <template #title> {{ card.title }} </template>
        <template #description>
          {{ card.description }}
        </template>
      </BaseCard>
    </div>
  </div>
</template>
