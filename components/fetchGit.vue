<script setup>
import { ref } from 'vue';

const username = ref('octocat'); // GitHub 用戶名稱
const userInfo = ref(null);
const isLoading = ref(false);
const error = ref(null);

const fetchUser = async () => {
    isLoading.value = true;
    error.value = null;

    try {
        const response = await fetch(`https://api.github.com/users/${username.value}`);
        if (!response.ok) throw new Error('無法獲取用戶資訊');

        userInfo.value = await response.json();
    } catch (err) {
        error.value = err.message;
    } finally {
        isLoading.value = false;
    }
};
</script>

<template>
    <div class="p-4">
        <input v-model="username" placeholder="輸入 GitHub 用戶名" class="border p-2 rounded" />
        <button @click="fetchUser" class="ml-2 bg-blue-500 text-white px-4 py-2 rounded">查詢</button>

        <div v-if="isLoading" class="mt-4">載入中...</div>
        <div v-if="error" class="mt-4 text-red-500">{{ error }}</div>

        <div v-if="userInfo" class="mt-4 border p-4 rounded bg-gray-100">
            <img :src="userInfo.avatar_url" alt="頭像" class="w-24 h-24 rounded-full">
            <h2 class="text-xl font-bold">{{ userInfo.name || userInfo.login }}</h2>
            <p class="text-gray-600">@{{ userInfo.login }}</p>
            <p class="mt-2">{{ userInfo.bio }}</p>
            <p class="mt-2">📍 {{ userInfo.location || '未知地點' }}</p>
            <a :href="userInfo.html_url" target="_blank" class="text-blue-500 mt-2 inline-block">查看 GitHub</a>
            {{ userInfo }}
        </div>
    </div>
</template>