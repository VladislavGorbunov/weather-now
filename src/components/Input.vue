<script setup>
import { ref } from 'vue';

let city = ref('');
let citySearch = ref()
let citys


function success(data) {
    
    
    fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${data.coords.latitude}&lon=${data.coords.longitude}&appid=47446ec5c14e2c7d955f3bf528f63b58&units=metric`)
    .then(res => res.json())
    .then((data) => {
        console.log(data)
        loading.value = false
        weather.value = data
    })
}

function error(data) {
    console.log('error', data)
}


function getWeather(e) {
    if (e.target.value.length > 1) {
        let res = geoCoding(e.target.value)

        res.then((res) => res.json())
        .then((data) => {
            console.log(data)
            for (let a of data) {
                if (a.hasOwnProperty('name')) {
                    //citySearch.value = []
                    citySearch.value.push(a)
                }
            }
            
            console.log(citySearch)
        })
        
        // citySearch.value = cities.filter((elem) => {
        //     return elem.name.startsWith(e.target.value)
        // })
    } else {
        citySearch.value = []
    }
}

function selectCityList(e) {
    city.value = e.target.textContent
    citySearch.value = []
    geoCoding(city)
}


function geoCoding() {
    //console.log(city.value)
    return fetch(`http://api.openweathermap.org/geo/1.0/direct?q=${city.value},ru&limit=6&appid=47446ec5c14e2c7d955f3bf528f63b58`)
}

</script>

<template>
    
    <!-- <div class="input-group mt-5">
        <input type="text" class="form-control cityInput" placeholder="Введите название города" v-model="city" v-on:input="getWeather">
        <button @click="geoCoding" class="btn btn-success btn-search" type="button" id="button-addon2"><i class="bi bi-cursor"></i> Смотреть</button>
    </div>
    <ul class="list-group mt-2">
        <li v-for="name in citySearch" @click="selectCityList" class="list-group-item">{{ name.name }}</li>
    </ul> -->
    
</template>

<style>
    
    .cityInput {
        border: none;
    }

    .btn-search {
        background: rgb(7, 85, 241) !important;
        border: none;
    }
</style>