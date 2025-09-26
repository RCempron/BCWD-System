<script setup>
import { ref } from 'vue'
const theme = ref('light')

function onClick() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

const icons = ['mdi-facebook', 'mdi-twitter', 'mdi-linkedin', 'mdi-instagram']gi
</script>

<template>
  <v-responsive class="border rounded">
    <v-app :theme="theme">
      <!-- App Bar -->
      <v-app-bar class="px-4 d-flex align-center" color="blue-lighten-1">
        <!-- Logo / App Name -->
        <div>
          <h2 class="font-weight-bold mb-0">
            <span class="text-primary">BCWD </span
            ><span class="text-black">LEAK COMPLAINT SYSTEM</span>
          </h2>
        </div>
        <v-spacer></v-spacer>
        <v-btn
          :prepend-icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'"
          slim
          size="large"
          @click="onClick"
        ></v-btn>
      </v-app-bar>

      <!-- Main Content -->
      <v-main>
        <v-container class="d-flex justify-center align-center fill-height">
          <slot name="content"></slot>
        </v-container>
      </v-main>

      <!-- Footer -->
      <v-footer app class="text-center d-flex flex-column ga-2 py-2" color="blue-lighten-2">
        <div class="d-flex ga-3">
          <v-btn
            v-for="icon in icons"
            :key="icon"
            :icon="icon"
            density="comfortable"
            variant="text"
          ></v-btn>
        </div>
      </v-footer>
    </v-app>
  </v-responsive>
</template>
