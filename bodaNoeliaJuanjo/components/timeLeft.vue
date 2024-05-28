<template>
  <v-container>
    <v-card>
      <v-card-title class="text-center">
        <p class="font-italic">Cuanto falta para la boda</p>
      </v-card-title>
      <v-divider></v-divider>
      <v-card-text>
        <div>
          <v-row align="start">
            <v-col
              v-for="n in 4"
              :key="n"
            >
              <v-sheet class="pa-1 ma-1" align="center">
                {{arrStringOfTable[n-1]}}
              </v-sheet>
              <v-sheet class="pa-1 ma-1" align="center">
                {{ formattedTime[n-1] }}
              </v-sheet>
            </v-col>
          </v-row>
        </div>
        <br>
        <v-progress-linear
          bg-color="surface-variant"
          class="mb-6"
          color="primary"
          height="10"
          v-bind:model-value="dias"
          rounded="pill"
        ></v-progress-linear>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script setup>
  import { ref, computed, onMounted, onBeforeUnmount } from 'vue';
  import { differenceInDays } from "date-fns";

  const arrStringOfTable = ['Días', 'Horas', 'Minutos', 'Segundos'];
  const CELEBRATION_DATE = '2025-09-12';

  const targetTime = new Date("2025-09-12T18:30:00").getTime();
  const currentTime = ref(new Date().getTime());
  const timeRemaining = ref(targetTime - currentTime.value);

  const formattedTime = computed(() => {

    const seconds = Math.floor(timeRemaining.value / 1000);
    const minutes = Math.floor(seconds / 60);
    const hours = Math.floor(minutes / 60);
    const days = Math.floor(hours / 24);
    return [days, hours % 24, minutes % 60, seconds % 60];

  });

  let dias = 100 - (differenceInDays(new Date(CELEBRATION_DATE), new Date()) * 100 / 500);

  onMounted(() => {

    intervalId = setInterval(updateTimer, 1000);

  });

  onBeforeUnmount(() => {

    clearInterval(intervalId);

  });

  function updateTimer() {

    currentTime.value = new Date().getTime();
    timeRemaining.value = Math.max(0, targetTime - currentTime.value);

  }
</script>
