<script setup>
import { ref, reactive } from 'vue';
import PersonalSetting from '~/components/personalSetting.vue';
import BusinessCard from '~/components/businessCard.vue';
import fetchGit from '~/components/fetchGit.vue';

useHead({
    title: "我的 Nuxt 頁面",
    link: [
        {
            rel: "stylesheet",
            href: "https://cdn.jsdelivr.net/npm/pagedone@1.2.2/src/css/pagedone.css"
        }
    ],
    script: [
        {
            src: "https://cdn.jsdelivr.net/npm/pagedone@1.2.2/src/js/pagedone.js",
            async: true
        }
    ]
});
const title = ref('某某');
const flipped = ref(false);

const businessCard = reactive({
    input: {
        personAttribute: [
            { label: "full name", name: "full", palceholder: "", type: "text" },
            { label: "nick name", name: "nick", palceholder: "", type: "text" },
            { label: "photo", name: "photo", palceholder: "", type: "file" },
        ],
        authority: [
            { label: "phone", name: "phone", palceholder: "", type: "tel" },
            { label: "email", name: "email", palceholder: "", type: "email" },
            { label: "company", name: "company", palceholder: "", type: "text" },
            { label: "location", name: "location", palceholder: "", type: "text" },
            { label: "website", name: "website", palceholder: "", type: "url" },
        ],
        socialMedia: [
            { label: "facebook", name: "facebook", palceholder: "", type: "text" },
            { label: "instagram", name: "instagram", palceholder: "", type: "text" },
        ]
    }
})
const person = reactive({
    personAttribute: {
        full: "我",
        parall: "jerry",
        nick: "jerry"
    },
    photo: "https://avatars.githubusercontent.com/u/87906523?v=4",
    birth: "1995/05/30",
    gender: "male",
    authority: {
        location: "新北市",
        company: "測試公司地址",
        phone: "1111",
        email: "test@gmail.com",
        website: "test.comm"
    },
    socialMedia: {
        facebook: "aaaa",
        instagram: "jerry29_new_life"
    },
    introduce: "測試",
    sign: "aaa"
})

</script>
<template>
    <div class="flex flex-grow gap-2 bg-gradient-to-br from-slate-900 to-cyan-600 h-screen p-2">
        <div class="w-1/4 h-full flex flex-col">
            <div class="text-2xl text-white font-bold p-2">Settings</div>
            <PersonalSetting :business-card="businessCard" :person="person" class="h-full overflow-y-auto" />
        </div>
        <div class="flex justify-center items-center flex-grow border-white border rounded-lg backdrop-blur-xs"
            @click="flipped = !flipped">
            <BusinessCard :business-card="businessCard" :person="person" />
        </div>
        <div>
            <!-- <fetchGit /> -->
        </div>
    </div>
</template>
