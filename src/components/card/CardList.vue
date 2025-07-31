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
  <div class="space-y-6">
    <div class="flex flex-col sm:flex-row gap-1 items-center justify-start">
      <div class="mt-2 flex">
        <div class="-mr-px grid grow grid-cols-1 focus-within:relative">
          <input
            type="text"
            name="query"
            id="query"
            class="col-start-1 row-start-1 block w-full rounded-l-md bg-white py-1.5 pr-3 pl-3 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-primary sm:pl-3 sm:text-sm/6"
            placeholder="캐릭터 검색"
          />
        </div>
        <button
          type="button"
          class="flex shrink-0 items-center gap-x-1.5 rounded-r-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 outline-1 -outline-offset-1 outline-gray-300 hover:bg-gray-50 focus:relative focus:outline-2 focus:-outline-offset-2 focus:outline-primary"
        >
          Search
        </button>
      </div>
    </div>

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
  </div>
</template>
