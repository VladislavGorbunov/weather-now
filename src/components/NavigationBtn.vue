<script setup>
import { ref } from 'vue';


const model = defineModel('nav');
const loading = defineModel('loading');

function navigation() {

    if (navigator.geolocation) {

        loading.value = true

        navigator.geolocation.getCurrentPosition((data) => {
            // model.value = getCoords(data)

            getWeather(data)
                .then((res) => res.json())
                .then((data) => {
                    model.value = data
                    loading.value = false
                })
        }, error)
    }
}

function error() {
    loading.value = false
}

function getWeather(data) {
    return fetch(`http://api.weatherapi.com/v1/current.json?key=5d6097650f9f4520909191040220804&q=${data.coords.latitude},${data.coords.longitude}&lang=ru`)
}

</script>

<template>
    <button @click="navigation" class="mt-3 navigation"><i class="bi bi-cursor-fill"></i> Определить город</button>
</template>

<style scoped>
.navigation {
    border: 1px solid rgba(0, 0, 0, 0.1) !important;
    padding: 10px 20px;
    border-radius: 35px 15px;
    background: rgba(14, 14, 15, 0.9) !important;
    width: 220px;
    color: #fff !important;
}
</style>