<template>
  <div class="music-generator">
    <div class="prompt-input">
      <textarea
        v-model="prompt"
        placeholder="음악 생성을 위한 프롬프트를 입력하세요..."
        class="w-full p-4 border-2 border-gray-300 rounded-lg focus:outline-none focus:border-blue-500"
        rows="4"
      ></textarea>
      <button
        @click="generateMusic"
        :disabled="isGenerating"
        class="mt-4 px-6 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 disabled:bg-gray-400"
      >
        {{ isGenerating ? '음악 생성 중...' : '음악 생성하기' }}
      </button>
    </div>

    <div v-if="generatedMusic" class="mt-8">
      <h3 class="text-xl font-bold mb-4">생성된 음악</h3>
      <audio :src="generatedMusic.audio_url" controls class="w-full"></audio>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';
import { useBookStore } from '@/stores/books';

const store = useBookStore();
const prompt = ref('');
const isGenerating = ref(false);
const generatedMusic = ref(null);

const generateMusic = async () => {
  if (!prompt.value.trim()) {
    alert('프롬프트를 입력해주세요.');
    return;
  }

  try {
    isGenerating.value = true;
    const response = await axios.post(
      `${store.API_URL}/api/songs/generate/`,
      { prompt: prompt.value },
      {
        headers: {
          Authorization: `Bearer ${localStorage.getItem('access')}`
        }
      }
    );
    generatedMusic.value = response.data;
  } catch (error) {
    console.error('음악 생성 실패:', error);
    alert('음악 생성에 실패했습니다. 다시 시도해주세요.');
  } finally {
    isGenerating.value = false;
  }
};
</script>

<style scoped>
.music-generator {
  max-width: 800px;
  margin: 0 auto;
  padding: 2rem;
}
</style> 