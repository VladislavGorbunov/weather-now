<script setup>
const props = defineProps(['navModel']);
import { ref } from 'vue';


</script>

<template>
  
  <h3 class="text-center"><span v-if="navModel.location?.name">В {{ navModel.location?.name }} сейчас {{ navModel.current?.condition.text.toLowerCase() }}</span></h3>

  <div class="col-12 weatherBlock mt-3" v-if="navModel.location?.name">

    <div class="row">
      <div class="col-12 col-md-4 text-center">
        <div class="p-3 weather-data-col">
          <span class="large-font"><i class="bi bi-thermometer-half"></i> {{ navModel.current?.temp_c }} °</span>
          <br />
          <span>Температура</span>
        </div>
      </div>

      <div class="col-12 col-md-4  text-center">
        <div class="p-3 weather-data-col">
          <span class="large-font"><i class="bi bi-droplet"></i> {{ navModel.current?.humidity }}%</span>
          <br />
          <span>Влажность</span>
        </div>
      </div>

      <div class="col-12 col-md-4  text-center">
        <div class="p-3 weather-data-col">
          <span class="large-font"><i class="bi bi-escape"></i> {{ navModel.current?.pressure_mb * 0.75 }} </span>
          <br />
          <span>Давление (мм рт. ст.)</span>
        </div>
      </div>

    </div>
  </div>
</template>


<style scoped>
.navigation {
  background: none;
  border: none;
  color: inherit;
}

.weatherBlock {
  font-size: 16px;
}

.large-font {
  font-size: 28px;
  font-weight: 700;
}

.weather-data-col {
  background: rgba(0, 0, 0, 0.05);
  border-radius: 20px;
}
</style>