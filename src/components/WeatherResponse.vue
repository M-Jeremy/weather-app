<script setup>
defineProps({
    weatherData: {
        type: Object,
        required: true
    },
    message: {
        type: String,
        required: false
    }
})
</script>

<template>
    <div v-if="Object.keys(weatherData).length !== 0 && message == ''" class="bg-blue-100 shadow-md rounded-lg p-6">
        <div class="flex flex-row gap-4">
            <div class="flex-1 bg-white p-4 rounded-lg shadow-inner mb-4">
                <p class="text-4xl font-semibold text-center">{{ weatherData.main.temp }}°C</p>
                <div class="flex justify-between mt-2 text-gray-500 text-sm">
                    <p>Min: {{ weatherData.main.temp_min }}°C</p>
                    <p>Max: {{ weatherData.main.temp_max }}°C</p>
                </div>
            </div>
            <div class="flex-1 bg-white p-4 rounded-lg shadow-inner mb-4">
                <p class="text-lg text-center">Humidité</p>
                <p class="text-2xl font-semibold text-center">{{ weatherData.main.humidity }}%</p>
            </div>
        </div>
        <div class="flex flex-col align-middle flex-1 bg-white p-4 rounded-lg shadow-inner">
            <p class="text-lg text-center">Météo</p>
            <div class="flex flex-row items-center justify-center gap-4">
                <p class="text-2xl font-semibold text-center capitalize">{{ weatherData.weather[0].description
                    }}</p>
                <img :src="`https://openweathermap.org/img/w/${weatherData.weather[0].icon}.png`" class="">
            </div>
        </div>
    </div>
    <div v-else-if="message !== ''" class="bg-red-100 shadow-md rounded-lg p-6">
        <p class="text-center">{{ message }}</p>
    </div>
</template>

<style scoped></style>