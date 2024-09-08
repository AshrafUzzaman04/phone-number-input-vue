<script setup>
import { ref, watch } from "vue";
import CountryCodePicker from "./countryCodePicker.vue";

const phoneCountry = defineModel("phoneCountry", {
    type: String,
});
const phoneNumber = defineModel("phoneNumber", {
    type: [Number, String],
});

const inputNumber = ref("");
const selectedCountry = ref("");

const updateValues = () => {
    phoneCountry.value = selectedCountry.value.code;
    phoneNumber.value = selectedCountry.value.dial_code + inputNumber.value;
};

const updateSelectedCountry = (country) => {
    selectedCountry.value = country
    updateValues();
}


watch([phoneNumber, selectedCountry], ([newPhone, newCountry], [prevPhone, prevCountry]) => {
    if (newPhone) {
        inputNumber.value = newPhone.substring(
            String(prevCountry ? prevCountry.dial_code : newCountry.dial_code).length,
            newPhone.length
        );
        updateValues();
    }
})

</script>

<template>
    <form class="max-w-lg mx-2 mx-md-auto">
        <div class="grid grid-cols-3">
            <CountryCodePicker :default-country="phoneCountry" @update="updateSelectedCountry" />
            <input v-model="inputNumber" @input="updateValues()" type="number" id="website-admin"
                class="rounded-none rounded-e-lg col-span-2 bg-gray-50 border border-gray-300 text-gray-900 focus:ring-blue-500 focus:border-blue-500 block flex-1 min-w-0 w-full text-sm p-2.5  dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Phone Number">
        </div>
    </form>
</template>

<style scoped lang='scss'></style>