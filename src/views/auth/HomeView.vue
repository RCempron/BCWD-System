<script setup>
import { ref } from 'vue'

const theme = ref('light')

function toggleTheme() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

function handleLocation(choice) {
  console.log('User selected:', choice)
}
</script>

<template>
  <v-responsive class="border rounded">
    <v-app :theme="theme">
      <!-- App Bar -->
      <v-app-bar color="blue" class="px-4">
        <h2 class="text-white font-weight-bold mb-0">Leak<span class="text-black">Alert</span></h2>
        <v-spacer></v-spacer>
        <v-btn
          :prepend-icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'"
          slim
          size="large"
          @click="toggleTheme"
        ></v-btn>
      </v-app-bar>

      <!-- Main Content -->
      <v-main>
        <v-container class="d-flex justify-center align-center fill-height">
          <v-card class="pa-6 text-center" max-width="420" outlined>
            <!-- Title -->
            <v-icon size="28" color="black" class="mb-2">mdi-map-marker</v-icon>
            <h3 class="mb-4">
              Allow <strong>LeakAlert</strong> to access <br />
              this device's location?
            </h3>

            <!-- Map Options -->
            <div class="d-flex justify-space-around mb-6">
              <div>
                <v-avatar size="100" class="mb-2" color="green-lighten-5">
                  <v-icon size="48" color="green">mdi-crosshairs-gps</v-icon>
                </v-avatar>
                <div>Precise</div>
              </div>

              <div>
                <v-avatar size="100" class="mb-2" color="grey-lighten-3">
                  <v-icon size="48" color="grey">mdi-crosshairs</v-icon>
                </v-avatar>
                <div>Approximate</div>
              </div>
            </div>

            <!-- Buttons -->
            <v-btn block color="blue" class="mb-3" @click="handleLocation('allow')">Allow</v-btn>
            <v-btn
              block
              variant="outlined"
              color="blue"
              class="mb-3"
              @click="handleLocation('once')"
              >Only this time</v-btn
            >
            <v-btn block variant="outlined" color="grey" @click="handleLocation('deny')"
              >Don't allow</v-btn
            >
          </v-card>
        </v-container>
      </v-main>

      <!-- Bottom Navigation -->
      <v-footer app class="pa-0">
        <v-bottom-navigation grow background-color="blue-lighten-5">
          <v-btn>
            <v-icon>mdi-menu</v-icon>
          </v-btn>
          <v-btn>
            <v-icon>mdi-home</v-icon>
            <span>Home</span>
          </v-btn>
          <v-btn>
            <v-icon>mdi-cog</v-icon>
            <span>Setting</span>
          </v-btn>
        </v-bottom-navigation>
      </v-footer>

      <!-- Floating Action Button -->
      <v-btn
        class="position-absolute"
        style="bottom: 80px; right: 20px"
        color="blue"
        size="large"
        icon
      >
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </v-app>
  </v-responsive>
</template>

<style scoped>
.text-black {
  color: #000;
}
</style>
