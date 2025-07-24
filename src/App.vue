<script setup lang="ts">
import NavigationBar from '@/components/menu/NavigationBar.vue'
</script>

<template>
  <div class="min-h-full">
    <NavigationBar />

    <!-- 메인 -->
    <RouterView />
  </div>
</template>
