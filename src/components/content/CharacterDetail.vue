<template>
  <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
    <!-- 2컬럼 레이아웃 -->
    <div class="lg:grid lg:grid-cols-2 lg:gap-0">
      <!-- 왼쪽: 캐릭터 이미지 (큰 화면에서만) -->
      <div class="hidden lg:block lg:bg-gray-50">
        <div class="flex h-full items-center justify-center p-8">
          <div class="relative">
            <img
              :src="props.characterData?.image || '/image/character/jin.webp'"
              :alt="props.characterData?.title || 'Character'"
              class="h-80 w-80 rounded-lg object-cover shadow-lg ring-4 ring-white"
              :style="{
                objectPosition: `0% ${props.characterData?.imgPosition || 25}%`,
                transform: `scale(${props.characterData?.imgScale || 1})`,
              }"
            />
          </div>
        </div>
      </div>

      <!-- 오른쪽: 캐릭터 정보 -->
      <div class="lg:col-span-1">
        <!-- 모바일용 캐릭터 헤더 -->
        <div class="flex items-center space-x-4 px-4 py-6 sm:px-6 lg:hidden">
          <img
            :src="props.characterData?.image || '/image/character/jin.webp'"
            :alt="props.characterData?.title || 'Character'"
            class="h-16 w-16 rounded-lg object-cover"
            :style="{
              objectPosition: `0% ${props.characterData?.imgPosition || 25}%`,
              transform: `scale(${props.characterData?.imgScale || 1})`,
            }"
          />
          <div>
            <h3 class="text-base/7 font-semibold text-gray-900">
              {{ props.characterData?.title || '캐릭터 이름' }}
            </h3>
            <p class="mt-1 text-sm/6 text-gray-500">
              {{ props.characterData?.description || '캐릭터 설명' }}
            </p>
          </div>
        </div>

        <!-- 데스크톱용 헤더 -->
        <div class="hidden px-4 py-6 sm:px-6 lg:block">
          <h3 class="text-base/7 font-semibold text-gray-900">
            {{ props.characterData?.title || '캐릭터 정보' }}
          </h3>
          <p class="mt-1 max-w-2xl text-sm/6 text-gray-500">
            {{ props.characterData?.description || '캐릭터 상세 정보' }}
          </p>
        </div>

        <!-- 상세 정보 섹션 -->
        <div class="border-t border-gray-100 lg:border-t-0">
          <dl class="divide-y divide-gray-100">
            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
              <dt class="text-sm font-medium text-gray-900">캐릭터 이름</dt>
              <dd class="mt-1 text-sm/6 text-gray-700 sm:col-span-2 sm:mt-0">
                {{ props.characterData?.title || '미상' }}
              </dd>
            </div>

            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
              <dt class="text-sm font-medium text-gray-900">캐릭터 ID</dt>
              <dd class="mt-1 text-sm/6 text-gray-700 sm:col-span-2 sm:mt-0">
                {{ props.characterData?.id || '미상' }}
              </dd>
            </div>

            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
              <dt class="text-sm font-medium text-gray-900">설명</dt>
              <dd class="mt-1 text-sm/6 text-gray-700 sm:col-span-2 sm:mt-0">
                {{ props.characterData?.description || '캐릭터에 대한 설명이 없습니다.' }}
              </dd>
            </div>

            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
              <dt class="text-sm font-medium text-gray-900">이미지 위치</dt>
              <dd class="mt-1 text-sm/6 text-gray-700 sm:col-span-2 sm:mt-0">
                {{ props.characterData?.imgPosition || 0 }}%
              </dd>
            </div>

            <div class="px-4 py-6 sm:grid sm:grid-cols-3 sm:gap-4 sm:px-6">
              <dt class="text-sm font-medium text-gray-900">이미지 스케일</dt>
              <dd class="mt-1 text-sm/6 text-gray-700 sm:col-span-2 sm:mt-0">
                {{ props.characterData?.imgScale || 1 }}x
              </dd>
            </div>
          </dl>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
interface CardData {
  id: string
  title: string
  description: string
  image: string
  imgPosition: number
  imgScale: number
}

interface Props {
  characterData?: CardData | null
}

const props = withDefaults(defineProps<Props>(), {
  characterData: null,
})
</script>
