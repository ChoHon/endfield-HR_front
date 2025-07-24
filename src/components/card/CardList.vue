<script setup lang="ts">
import BaseCard from '@/components/card/BaseCard.vue'
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

interface CardData {
  id: number
  title: string
  description: string
  image: string
  imgPosition: number
  imgScale: number
}

const router = useRouter()
const cards = ref<CardData[]>([])

// 카드 클릭 핸들러
const handleCardClick = (card: CardData) => {
  router.push(`/character/${card.id}`)
}

// JSON 파일에서 데이터 로드
const loadCards = async () => {
  try {
    const response = await fetch('/data/cards.json')
    cards.value = await response.json()
  } catch (error) {
    console.error('카드 데이터 로드 실패:', error)
  }
}

onMounted(loadCards)
</script>

<template>
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
    <div v-for="card in cards" :key="card.id">
      <BaseCard hoverable @click="handleCardClick(card)">
        <template #image>
          <img
            :src="card.image"
            alt="card image"
            class="w-full h-full object-cover transition-transform duration-300 hover:scale-105"
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
