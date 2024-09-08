<script setup>
import { reactive, ref } from "vue";
import PhoneNumberInput from "./components/phoneNumberInput.vue"

const phone = ref({
  phone_country: "bd",
  phone_number: "",
})
</script>

<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-white dark:bg-gray-800">
    <!-- :phone-number="phone.phone_number" :phone-country="phone.phone_country"  -->
    <PhoneNumberInput v-model:phone-number="phone.phone_number" v-model:phone-country="phone.phone_country" />
    <div class="flex gap-2 my-2 text-black dark:text-white">
      <span>{{ phone.phone_country }}</span>
      <span>{{ phone.phone_number }}</span>
    </div>
  </div>
</template>

<style scoped lang='scss'></style>