<script setup>
import { ref } from 'vue'
const theme = ref('light')

function onClick() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

const icons = ['mdi-facebook', 'mdi-twitter', 'mdi-linkedin', 'mdi-instagram']

// Form fields
const username = ref('')
const email = ref('')
const phone = ref('')
const password = ref('')
const showPassword = ref(false)

function register() {
  console.log('Username:', username.value)
  console.log('Email:', email.value)
  console.log('Phone:', phone.value)
  console.log('Password:', password.value)
}
</script>

<template>
  <v-responsive class="border rounded">
    <v-app :theme="theme">
      <!-- App Bar -->
      <v-app-bar class="px-4 d-flex align-center" color="blue-lighten-1">
        <!-- Logo / App Name -->
        <div>
          <h2 class="font-weight-bold mb-0">
            <span class="text-primary">Leak</span><span class="text-black">Alert</span>
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
          <v-card class="pa-6" max-width="400" elevation="0">
            <!-- Title -->
            <div class="text-center mb-6">
              <h2 class="font-weight-bold">Create an account</h2>
            </div>

            <!-- Register Form -->
            <v-form>
              <!-- Username -->
              <v-text-field
                v-model="username"
                label="Username"
                placeholder="Enter Your Username"
                outlined
                dense
                class="mb-3"
              />

              <!-- Email -->
              <v-text-field
                v-model="email"
                label="Email"
                type="email"
                placeholder="Enter Your Email"
                outlined
                dense
                class="mb-3"
              />

              <!-- Phone Number -->
              <v-text-field
                v-model="phone"
                label="Phone Number"
                type="tel"
                placeholder="Enter Your Phone Number"
                outlined
                dense
                class="mb-3"
              />

              <!-- Password -->
              <v-text-field
                v-model="password"
                :type="showPassword ? 'text' : 'password'"
                label="Password"
                placeholder="Enter Your Password"
                outlined
                dense
                class="mb-2"
                :append-inner-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
                @click:append-inner="showPassword = !showPassword"
              />

              <!-- Sign Up Button -->
              <v-btn block color="primary" class="mb-4" height="45" @click="register">
                Sign Up
              </v-btn>

              <!-- Divider with text -->
              <div class="d-flex align-center mb-4">
                <v-divider class="flex-grow-1"></v-divider>
                <span class="mx-2 text-center">or</span>
                <v-divider class="flex-grow-1"></v-divider>
              </div>

              <!-- Social Sign Up -->
              <v-btn
                block
                color="blue darken-1"
                class="mb-2"
                height="45"
                prepend-icon="mdi-facebook"
                href="https://www.facebook.com"
              >
                Signup with Facebook
              </v-btn>
              <v-btn
                block
                variant="outlined"
                color="grey"
                height="45"
                prepend-icon="mdi-google"
                href="https://accounts.google.com"
              >
                Signup with Google
              </v-btn>

              <!-- Already have an account -->
              <div class="text-center mt-4">
                Already have an account?
                <RouterLink to="/login" class="text-blue text-decoration-none">Login</RouterLink>
              </div>
            </v-form>
          </v-card>
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

<style scoped>
.text-blue {
  color: #1976d2;
}
.text-red {
  color: #e53935;
}
.text-small {
  font-size: 12px;
}
</style>
