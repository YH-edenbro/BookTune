<template>
  <div class="rounded-box flex flex-col items-center justify-center p-6 min-h-[340px]">
    <span class="section-title mb-2 text-lg">책 커버 이미지</span>
    <img :src="cover || 'https://placehold.co/220x300?text=Book+Cover'" :alt="title" class="rounded-lg shadow-md border border-gray-200 mt-2">
  </div>
</template>

<script setup>
defineProps({
  cover: {
    type: String,
    default: ''
  },
  title: {
    type: String,
    default: ''
  }
})
</script>

<style scoped>
.rounded-box {
  border: 2.5px solid #222;
  border-radius: 1rem;
  background: #fff;
  box-shadow: 0 2px 8px 0 rgba(0,0,0,0.03);
}

.section-title {
  font-family: 'Noto Sans KR', sans-serif;
  font-weight: 700;
  font-size: 1.1rem;
  color: #222;
}
</style> 