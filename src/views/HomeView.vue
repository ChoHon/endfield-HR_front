<script setup lang="ts">
import HeaderDescription from '@/components/header/HeaderDescription.vue'
import CardList from '@/components/card/CardList.vue'
</script>

<template>
  <div class="py-10">
    <header>
      <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
        <HeaderDescription>
          <template #title>하잉</template>
          <template #description>주절주절</template>
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
