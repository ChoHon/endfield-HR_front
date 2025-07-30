<template>
  <div class="bg-white">
    <!-- 캐릭터 이미지 -->
    <div class="flex w-full justify-center">
      <img
        :src="props.characterData?.image"
        :alt="props.characterData?.title"
        class="max-w-none flex-shrink-0 -mb-20"
        style="transform: scale(0.8) translateY(10px); transform-origin: top center"
      />
    </div>

    <!-- 캐릭터 정보 -->
    <div>
      <!-- 테이블 -->
      <div class="mt-2 border-t border-gray-100">
        <dl class="grid grid-cols-1 sm:grid-cols-2">
          <div class="border-t border-gray-100 px-4 py-6 sm:col-span-1 sm:px-0">
            <dt class="text-sm/6 font-medium text-gray-900">Full name</dt>
            <dd class="mt-1 text-sm/6 text-gray-700 sm:mt-2">Margot Foster</dd>
          </div>
          <div class="border-t border-gray-100 px-4 py-6 sm:col-span-1 sm:px-0">
            <dt class="text-sm/6 font-medium text-gray-900">Application for</dt>
            <dd class="mt-1 text-sm/6 text-gray-700 sm:mt-2">Backend Developer</dd>
          </div>
          <div class="border-t border-gray-100 px-4 py-6 sm:col-span-1 sm:px-0">
            <dt class="text-sm/6 font-medium text-gray-900">Email address</dt>
            <dd class="mt-1 text-sm/6 text-gray-700 sm:mt-2">margotfoster@example.com</dd>
          </div>
          <div class="border-t border-gray-100 px-4 py-6 sm:col-span-1 sm:px-0">
            <dt class="text-sm/6 font-medium text-gray-900">Salary expectation</dt>
            <dd class="mt-1 text-sm/6 text-gray-700 sm:mt-2">$120,000</dd>
          </div>
          <div class="border-t border-gray-100 px-4 py-6 sm:col-span-2 sm:px-0">
            <dt class="text-sm/6 font-medium text-gray-900">About</dt>
            <dd class="mt-1 text-sm/6 text-gray-700 sm:mt-2">
              Fugiat ipsum ipsum deserunt culpa aute sint do nostrud anim incididunt cillum culpa
              consequat. Excepteur qui ipsum aliquip consequat sint. Sit id mollit nulla mollit
              nostrud in ea officia proident. Irure nostrud pariatur mollit ad adipisicing
              reprehenderit deserunt qui eu.
            </dd>
          </div>
          <div class="border-t border-gray-100 px-4 py-6 sm:col-span-2 sm:px-0">
            <dt class="text-sm/6 font-medium text-gray-900">Attachments</dt>
            <dd class="mt-2 text-sm text-gray-900">
              <ul role="list" class="divide-y divide-gray-100 rounded-md border border-gray-200">
                <li class="flex items-center justify-between py-4 pr-5 pl-4 text-sm/6">
                  <div class="flex w-0 flex-1 items-center">
                    <PaperClipIcon class="size-5 shrink-0 text-gray-400" aria-hidden="true" />
                    <div class="ml-4 flex min-w-0 flex-1 gap-2">
                      <span class="truncate font-medium text-gray-900"
                        >resume_back_end_developer.pdf</span
                      >
                      <span class="shrink-0 text-gray-400">2.4mb</span>
                    </div>
                  </div>
                  <div class="ml-4 shrink-0">
                    <a href="#" class="font-medium text-indigo-600 hover:text-indigo-500"
                      >Download</a
                    >
                  </div>
                </li>
                <li class="flex items-center justify-between py-4 pr-5 pl-4 text-sm/6">
                  <div class="flex w-0 flex-1 items-center">
                    <PaperClipIcon class="size-5 shrink-0 text-gray-400" aria-hidden="true" />
                    <div class="ml-4 flex min-w-0 flex-1 gap-2">
                      <span class="truncate font-medium text-gray-900"
                        >coverletter_back_end_developer.pdf</span
                      >
                      <span class="shrink-0 text-gray-400">4.5mb</span>
                    </div>
                  </div>
                  <div class="ml-4 shrink-0">
                    <a href="#" class="font-medium text-indigo-600 hover:text-indigo-500"
                      >Download</a
                    >
                  </div>
                </li>
              </ul>
            </dd>
          </div>
        </dl>
      </div>
    </div>
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
