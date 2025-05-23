<template>
  <div v-if="$route.meta.layout !== 'none'" class="min-h-screen bg-gray-50">
    <!-- Header -->
    <header class="w-full flex items-center justify-between px-8 py-6 bg-white shadow-sm fixed top-0 left-0 right-0 z-10">
      <div class="flex items-center gap-8">
        <a href="#" class="nav-link text-gray-800">
          <RouterLink :to="{ name: 'home'}">Home</RouterLink>
        </a>
      </div>
      <div class="flex items-center gap-8">
        <div v-if="!isLoggedIn">
          <a href="#" class="nav-link text-gray-800" @click.prevent="openLoginPopup">Login</a>
          <span> | </span>
          <a href="#" class="nav-link text-gray-800" @click.prevent="openSignupPopup">Sign up</a>
        </div>
        <div v-else>
          <template v-if="nickname">
            <a href="#" class="nav-link text-gray-800" @click.prevent="goProfile">{{ nickname }}</a>
            <span> | </span>
            <a href="#" class="nav-link text-gray-800" @click.prevent="logout">Logout</a>
          </template>
        </div>
      </div>
    </header>
    <!-- 로그인/회원가입 팝업 -->
    <LoginView v-if="isLoginPopupVisible" @close-popup="closeLoginPopup" @login-success="checkLogin" />
    <SignupView v-if="isSignupPopupVisible" @close-popup="closeSignupPopup" @signup-success="checkLogin" />
    <!-- 로고/검색바: 모든 페이지에서 항상 보이게 -->
    <div class="flex flex-col items-center text-center pt-32">
      <span class="logo text-gray-900">BookTune</span>
      <span class="text-gray-500 mt-1 text-base tracking-wide">음악과 함께 즐기는 독서</span>
      <a href="#" class="nav-link text-gray-800">
        <RouterLink :to="{ name: 'BookList'}">Book List</RouterLink>
      </a>
      <form class="search-bar-container" @submit.prevent="onSearch">
        <input
          type="text"
          placeholder="책, 저자, 음악 검색..."
          class="search-input"
          v-model="searchKeyword"
        />
        <button class="search-btn" type="submit">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor" class="w-6 h-6">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19V6l12-2v13"/>
            <circle cx="9" cy="19" r="3" fill="currentColor"/>
            <circle cx="21" cy="17" r="3" fill="currentColor"/>
          </svg>
        </button>
      </form>
    </div>
    <RouterView />
  </div>
  <div v-else>
    <RouterView />
  </div>
</template>

<script setup>
import { ref, onMounted, onUpdated, nextTick, watch } from 'vue';
import { RouterView, RouterLink, useRoute } from 'vue-router';
import { useRouter } from 'vue-router';
import LoginView from './views/LoginView.vue';
import SignupView from './views/SignUpView.vue';
import axios from 'axios';
import { useBookStore } from '@/stores/books'

const isLoginPopupVisible = ref(false);
const isSignupPopupVisible = ref(false);
const searchKeyword = ref('');
const isLoggedIn = ref(false);
const store = useBookStore()
const nickname = ref('')
const router = useRouter();
const route = useRoute();

function openLoginPopup() {
  isLoginPopupVisible.value = true;
}
function closeLoginPopup() {
  isLoginPopupVisible.value = false;
  checkLogin();
}
function openSignupPopup() {
  isSignupPopupVisible.value = true;
}
function closeSignupPopup() {
  isSignupPopupVisible.value = false;
  checkLogin();
}
function onSearch() {
  if (searchKeyword.value.trim()) {
    router.push({ name: 'BookSearch', query: { q: searchKeyword.value.trim() } });
    searchKeyword.value = '';
  }
}
async function checkLogin() {
  try {
    const access = localStorage.getItem('access');
    if (access) {
      isLoggedIn.value = true;
      await nextTick()
      const profile = await getProfile()
      nickname.value = profile.nickname
    } else {
      isLoggedIn.value = false;
      nickname.value = '';
    }
  } catch (error) {
    console.error('Login check failed:', error);
    isLoggedIn.value = false;
    nickname.value = '';
  }
}
function goProfile() {
  router.push({ name: 'profile' });
}
function logout() {
  localStorage.removeItem('access');
  isLoggedIn.value = false;
  nickname.value = '';
  router.push({ name: 'home' });
}

onMounted(async () => {
  await checkLogin();
});

watch(
  () => route.fullPath,
  async () => {
    await checkLogin();
  }
);

const getProfile = async function () {
    try {
      const access = localStorage.getItem('access');
      const response = await axios({
        method: 'get',
        url: `${store.API_URL}/api/auth/profile/`,
        headers: { Authorization: `Bearer ${access}` } 
      })
      const result = response.data
      return result
    } catch (error) {
      console.error('No profile', error)
      throw error
    }
  }
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Indie+Flower&family=Noto+Sans+KR:wght@400;700&family=Pacifico&display=swap');

body {
  font-family: 'Noto Sans KR', sans-serif;
  background: #f7f8fa;
}
.logo {
  font-family: 'Indie Flower', cursive;
  font-size: 6rem;
  letter-spacing: 0.05em;
}
.section-title {
  font-family: 'Indie Flower', cursive;
  font-size: 3rem;
  letter-spacing: 0.03em;
  font-weight: bold;
}
.nav-link {
  font-family: 'Indie Flower', cursive;
  font-size: 2rem;
  transition: color 0.2s;
  font-weight: bold;
  color: #000000;
}
.nav-link:hover {
  color: #6366f1;
}
.nav-link:active {
  color: #6366f1;
}
.search-bar-container {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  max-width: 480px;
  margin: 3rem auto 0 auto;
  background: #fff;
  box-shadow: 0 2px 16px 0 rgba(0,0,0,0.07);
  padding: 0.25rem 0.5rem 0.25rem 1.2rem;
}
.search-input {
  flex: 1;
  border: 2.5px solid #ddd;
  outline: none;
  background: transparent;
  font-size: 1.1rem;
  padding: 0.8rem 1rem;
  border-radius: 0;
  text-align: center;
  transition: border 0.2s;
}
.search-input:focus {
  border: 2.5px solid #7bed9f;
}
.search-input::placeholder {
  color: #bbb;
  font-size: 1.1rem;
  text-align: center;
}
.search-btn {
  background: transparent;
  border: none;
  border-radius: 0;
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 0.5rem;
  cursor: pointer;
  transition: none;
  box-shadow: none;
}
.search-btn svg {
  color: #bbb;
  transition: color 0.2s;
}
.search-btn:hover svg {
  color: #7bed9f;
}
</style>