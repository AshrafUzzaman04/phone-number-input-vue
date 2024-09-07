<script setup>
import countries from "../utils/coutry.js";
import { computed, ref, watch } from 'vue';
import { Dropdown } from 'flowbite';

const $emit = defineEmits(['update'])

const props = defineProps({
    defaultCountry: String,
})

const selectedQuery = ref({});

const filteredCountries = computed(() => {
    return countries;
})

const selectedCountry = (country) => {
    selectedQuery.value = country;
    $emit('update', country)
}

watch(() => props.defaultCountry, () => {
    let country = countries[0];
    if (props.defaultCountry) {
        country = countries.filter(country => country.code.toString().toLocaleLowerCase() === props.defaultCountry.toString().toLocaleLowerCase())[0]
    }
    selectedCountry(country);
}, { immediate: true })
</script>

<template>
    <div class="inline-flex items-center px-3 text-sm text-gray-900 bg-gray-200 border border-gray-300 cursor-pointer min-w-1/3 border-e-0 rounded-s-md dark:bg-gray-600 dark:text-gray-400 dark:border-gray-600"
        id="dropdownSearchButton" data-dropdown-toggle="dropdownSearch" data-dropdown-placement="bottom-start">
        <button class="inline-flex items-center justify-between" type="button">
            {{ `${selectedQuery.flag} ${selectedQuery.dial_code}` }}
            <svg class="w-2.5 h-2.5 ms-3" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none"
                viewBox="0 0 10 6">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                    d="m1 1 4 4 4-4" />
            </svg>
        </button>

    </div>
    <!-- Dropdown menu -->
    <div id="dropdownSearch" class="z-10 hidden bg-white rounded-lg shadow w-60 dark:bg-gray-700">
        <div class="p-3">
            <label for="input-group-search" class="sr-only">Search</label>
            <div class="relative">
                <div class="absolute inset-y-0 flex items-center pointer-events-none rtl:inset-r-0 start-0 ps-3">
                    <svg class="w-4 h-4 text-gray-500 dark:text-gray-400" aria-hidden="true"
                        xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z" />
                    </svg>
                </div>
                <input type="text" id="input-group-search"
                    class="block w-full p-2 text-sm text-gray-900 border border-gray-300 rounded-lg ps-10 bg-gray-50 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Search user">
            </div>
        </div>
        <ul class="h-48 px-3 pb-3 overflow-auto text-sm text-gray-700 dark:text-gray-200"
            aria-labelledby="dropdownSearchButton">
            <li v-for="(country, i) in filteredCountries" :key="i" class="cursor-pointer"
                @click="selectedCountry(country)">
                <div
                    class="flex items-center rounded text-md ps-2 hover:bg-gray-100 dark:hover:bg-gray-600 whitespace-nowrap">
                    {{ country.flag + ' ' + country.dial_code + ' (' + country.code + ', ' + country.name + ')' }}
                </div>
            </li>
        </ul>
    </div>

</template>

<style scoped lang='scss'></style>