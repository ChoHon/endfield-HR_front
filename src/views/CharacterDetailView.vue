<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import { useRoute } from 'vue-router'
import HeaderDescription from '@/components/header/HeaderDescription.vue'
import CharacterDetail from '@/components/content/CharacterDetail.vue'

interface CardData {
  id: number
  title: string
  description: string
  image: string
}

const route = useRoute()
const cards = ref<CardData[]>([])
const characterId = computed(() => Number(route.params.id))

// 현재 캐릭터 데이터 찾기
const currentCharacter = computed(() => {
  return cards.value.find((card) => card.id === characterId.value)
})

// 카드 데이터 로드
const loadCards = async () => {
  try {
    const response = await fetch('/data/cards.json')
    cards.value = await response.json()
  } catch (error) {
    console.error('캐릭터 데이터 로드 실패:', error)
  }
}

onMounted(loadCards)
</script>

<template>
  <div class="py-10">
    <header>
      <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
        <!-- 뒤로가기 버튼 -->
        <div class="mb-4">
          <router-link
            to="/"
            class="inline-flex items-center px-4 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
          >
            <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M15 19l-7-7 7-7"
              />
            </svg>
            목록으로 돌아가기
          </router-link>
        </div>

        <HeaderDescription>
          <template #title>{{ currentCharacter?.title || '캐릭터 정보' }}</template>
          <template #description>{{
            currentCharacter?.description || '캐릭터 상세 정보를 확인하세요.'
          }}</template>
        </HeaderDescription>
      </div>
    </header>
    <main>
      <div class="mx-auto max-w-7xl px-4 py-8 sm:px-6 lg:px-8">
        <!-- 로딩 상태 -->
        <div v-if="!currentCharacter && cards.length === 0" class="flex justify-center py-10">
          <div class="animate-pulse text-gray-500">캐릭터 정보를 불러오고 있습니다...</div>
        </div>

        <!-- 캐릭터 없음 -->
        <div v-else-if="!currentCharacter && cards.length > 0" class="text-center py-10">
          <div class="text-gray-500 text-lg">캐릭터를 찾을 수 없습니다.</div>
          <router-link
            to="/"
            class="mt-4 inline-block px-4 py-2 bg-indigo-600 text-white rounded hover:bg-indigo-700"
          >
            목록으로 돌아가기
          </router-link>
        </div>

        <!-- 캐릭터 상세 정보 -->
        <CharacterDetail v-else :characterData="currentCharacter" />
      </div>
    </main>
  </div>
</template>
