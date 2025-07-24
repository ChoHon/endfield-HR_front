<script setup lang="ts">
import HeaderDescription from '@/components/header/HeaderDescription.vue'
import CardList from '@/components/card/CardList.vue'
</script>

<template>
  <div class="py-10">
    <header>
      <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
        <HeaderDescription>
          <template #title>캐릭터 목록</template>
          <template #description>원하는 캐릭터를 클릭해서 상세 정보를 확인해보세요.</template>
        </HeaderDescription>
      </div>
    </header>
    <main>
      <div class="mx-auto max-w-7xl px-4 py-8 sm:px-6 lg:px-8">
        <CardList />
      </div>
    </main>
  </div>
</template>
