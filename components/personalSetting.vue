<script setup>
import { defineProps } from 'vue';

const { person, businessCard } = defineProps({
    person: Object,
    businessCard: Object
});

function camelToKebab(str) {
    return str
        .replace(/([a-z0-9])([A-Z])/g, '$1 $2')
        .toLowerCase()
        .replace(/^(.)/, (match) => match.toUpperCase())
}

const notSingleInputTag = ["select", "radio", "checkbox", "textarea"]

</script>
<template>
    <div class="flex flex-col justify-evenly gap-2">
        <div v-for="(info, section) in businessCard.input" class="flex flex-col p-2 rounded-lg bg-black">
            <p class="text-xl text-white italic">
                {{ camelToKebab(section) }}
            </p>
            <div v-for="field in info" class="flex flex-col py-1.5" :key="field.title">
                <label for="" class="text-white font-thin">
                    {{ field.label }}
                </label>
                <input v-if="!notSingleInputTag.includes(field.type)" v-model="person[section][field.name]"
                    class="col-span-2 rounded-sm bg-slate-800 border-white border text-white" :name="field.name"
                    :placeholder="field.palceholder" :type="field.type">
                <select v-if="field.type == 'select'" class="text-white w-full h-fit">
                    <option v-for="option in field.options" :value="option" :key="option">{{ option }}</option>
                </select>
            </div>
        </div>
    </div>
</template>