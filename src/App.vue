<script setup>

import { RouterLink, RouterView } from 'vue-router';
import Logo from './components/Logo.vue';
import Input from './components/Input.vue';
import Loading from './components/Loading.vue';
import WeatherData from './components/WeatherData.vue';
import NavigationBtn from './components/NavigationBtn.vue';
import { ref } from 'vue';


let darkMode = ref(localStorage.darkMode)
const navModel = ref('')
const loading = ref(false)

function setTheme() {
  if (localStorage.darkMode == 1) {
    setDark()
  } else {
    setLight()
  }
}

function toggleTheme() {
  if (localStorage.darkMode == 1) {
    setLight()
  } else {
    setDark()
  }
}

function setDark() {
  darkMode.value = 1
  localStorage.darkMode = 1
}

function setLight() {
  darkMode.value = 0
  localStorage.darkMode = 0
}


setTheme()

</script>

<template>

  <div class="col-12 col-md-6  mx-auto bg-container p-5" :class="{ dark: darkMode }">
    <div class="blur-round"></div>
    <div class="row">
      <div class="col-12 col-md-6">
        <Logo />
      </div>

      <div class="col-12 col-md-6 d-flex align-items-center justify-content-center">
        <div class="d-flex align-items-center flex-column">
          <button @click="toggleTheme" class="btn btn-primary btn-select-theme">
            <i class="bi bi-brightness-high-fill" v-if="darkMode"></i>
            <i class="bi bi-moon-fill" v-else></i>
            Изменить тему
          </button>

          <NavigationBtn v-model:nav="navModel" v-model:loading="loading" />
        </div>
      </div>
    </div>

    <hr>
    <Loading v-if="loading" />
    <WeatherData :navModel="navModel" />

    <RouterView />
  </div>
</template>
