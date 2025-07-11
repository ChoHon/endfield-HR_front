<template>
  <div
    :class="[
      'overflow-hidden rounded-lg bg-white shadow-sm transition-shadow duration-200',
      hoverable ? 'hover:shadow-md cursor-pointer' : '',
      size === 'sm' ? 'text-sm' : '',
      size === 'lg' ? 'text-lg' : '',
      className,
    ]"
    @click="onClick"
  >
    <!-- 이미지 영역 -->
    <div v-if="$slots.image" class="aspect-video w-full overflow-hidden">
      <slot name="image" />
    </div>

    <!-- 메인 컨텐츠 -->
    <div :class="['px-4 py-5 sm:p-6', $slots.image ? 'pt-4' : '']">
      <!-- 헤더 영역 -->
      <div class="flex items-start justify-between">
        <div class="flex-1">
          <!-- 제목 -->
          <h3 v-if="title || $slots.title" class="text-lg font-medium text-gray-900">
            <slot name="title">{{ title }}</slot>
          </h3>

          <!-- 설명 -->
          <p v-if="description || $slots.description" class="mt-1 text-sm text-gray-500">
            <slot name="description">{{ description }}</slot>
          </p>
        </div>

        <!-- 우측 상단 액션 -->
        <div v-if="$slots.topAction" class="ml-4 flex-shrink-0">
          <slot name="topAction" />
        </div>
      </div>

      <!-- 메인 컨텐츠 -->
      <div v-if="$slots.content" class="mt-4">
        <slot name="content" />
      </div>

      <!-- 통계/메타 정보 -->
      <div v-if="$slots.stats" class="mt-4 border-t border-gray-200 pt-4">
        <slot name="stats" />
      </div>
    </div>

    <!-- 하단 액션 영역 -->
    <div v-if="$slots.actions" class="border-t border-gray-200 bg-gray-50 px-4 py-3 sm:px-6">
      <slot name="actions" />
    </div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  title?: string
  description?: string
  size?: 'sm' | 'md' | 'lg'
  hoverable?: boolean
  className?: string
}

const props = withDefaults(defineProps<Props>(), {
  size: 'md',
  hoverable: false,
  className: '',
})

const emit = defineEmits<{
  click: [event: MouseEvent]
}>()

const onClick = (event: MouseEvent) => {
  if (props.hoverable) {
    emit('click', event)
  }
}
</script>
