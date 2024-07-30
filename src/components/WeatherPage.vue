<template>
    <div class="flex flex-col gap-4 ml-16 mr-8">
        <div class="flex flex-col gap-4">
            <span class="text-lg">Affichage de la météo par ville
                <span class="text-xs"> alimenté par
                    <span class="text-orange-600">OpenWeatherMap</span>
                </span>
            </span>
            <div class="flex flex-row items-center gap-4">
                <div class="flex-1">
                    <input v-model="city" @keyup.enter="getData" type="text" required
                        placeholder="Rechercher une ville..."
                        class="w-full rounded-lg border-0 py-2 px-3 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600">
                </div>
                <div class="w-1/4">
                    <button type="submit" @click="getData"
                        class="flex w-full justify-center rounded-lg bg-indigo-600 py-1.5 font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Rechercher</button>
                </div>
            </div>
        </div>
        <div class="h-1/2 break-all rounded-lg">
            <WeatherResponse :weatherData="weatherData" :message="message" />
            <div v-if="loading">
                <br>
                <ScaleLoader color="#DBE9FE" />
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import ScaleLoader from 'vue-spinner/src/ScaleLoader.vue'

import WeatherResponse from './WeatherResponse.vue';

export default {
    name: 'WeatherPage',
    components: {
        WeatherResponse,
        ScaleLoader
    },
    data() {
        return {
            city: '',
            message: '',
            weatherData: {},
            loading: false
        };
    },
    methods: {
        getData: async function () {
            this.message = '';
            if (this.city === '') {
                this.message = 'Veuillez saisir une ville';
            } else {
                const req = `${import.meta.env.VITE_BASE_URL}?q=${this.city}&units=metric&${import.meta.env.VITE_OPEN_WEATHER_APP_ID}`;
                this.loading = true;
                await axios.get(req)
                    .then(response => {
                        this.city = response.data.name;
                        this.weatherData = response.data;
                    })
                    .catch(error => {
                        this.weatherData = {};
                        this.message = 'Ville non reconnue';
                        console.error(error);
                    })
                    .finally(() => { this.loading = false });
            }
        }
    }
};
</script>

<style scoped></style>