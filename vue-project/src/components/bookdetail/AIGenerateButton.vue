<template>
  <div class="w-full max-w-5xl flex justify-start mt-10">
    <button class="btn-ai-music px-10 py-5 shadow-lg" @click="showPopup">make AI MUSIC</button>
    <CreateMusicView v-if="isPopupVisible" @close-popup="closePopup" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import CreateMusicView from '@/views/CreateMusicView.vue';

const isPopupVisible = ref(false);

const showPopup = () => {
  isPopupVisible.value = true;
};

const closePopup = () => {
  isPopupVisible.value = false;
};
</script>

<style scoped>
.btn-ai-music {
  font-family: 'Inter', 'Noto Sans KR', sans-serif;
  font-size: 1.3rem;
  font-weight: 700;
  letter-spacing: 0.05em;
  background: linear-gradient(90deg, #6366f1 0%, #60a5fa 100%);
  color: #fff;
  border: none;
  border-radius: 0.75rem;
  box-shadow: 0 2px 8px 0 rgba(99,102,241,0.08);
  transition: background 0.2s, transform 0.1s;
}

.btn-ai-music:hover {
  background: linear-gradient(90deg, #4f46e5 0%, #2563eb 100%);
  transform: translateY(-2px) scale(1.03);
}
</style> 