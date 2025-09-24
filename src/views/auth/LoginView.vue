<script setup>
import { ref } from 'vue'
import { useRouter, RouterLink } from 'vue-router' // Import RouterLink

const router = useRouter()

const theme = ref('light')

function onClick() {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

const icons = ['mdi-facebook', 'mdi-twitter', 'mdi-linkedin', 'mdi-instagram']

const email = ref('')
const password = ref('')
const rememberMe = ref(false)
const showPassword = ref(false)

function login() {
  console.log('Email:', email.value)
  console.log('Password:', password.value)
  console.log('Remember Me:', rememberMe.value)
  router.push({ name: 'Dashboard' }) // Use router to navigate
}
</script>

<template>
  <v-responsive class="border rounded">
    <v-app :theme="theme">
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

      <v-main>
        <v-container class="d-flex justify-center align-center fill-height">
          <v-card class="pa-6" max-width="400" elevation="0">
            <!-- Title -->
            <div class="text-center mb-6">
              <h2 class="font-weight-bold">Hi, Welcome Back!</h2>
            </div>

            <!-- Login Form -->
            <v-form>
              <!-- Email -->
              <v-text-field
                v-model="email"
                label="Email"
                type="email"
                placeholder="example@gmail.com"
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

              <!-- Remember Me + Forgot Password -->
              <div class="d-flex justify-space-between align-center mb-4 text-small">
                <v-checkbox v-model="rememberMe" hide-details density="compact" class="text-small">
                  <template #label>
                    <span class="text-small">Remember Me</span>
                  </template>
                </v-checkbox>
                <a href="#" class="text-red text-decoration-none">Forgot Password?</a>
              </div>

              <!-- Login Button -->
              <v-btn block color="primary" class="mb-4" height="45" @click="login">
                <RouterLink to="/home">Login</RouterLink>
              </v-btn>

              <!-- Divider with text -->
              <div class="d-flex align-center mb-4">
                <v-divider class="flex-grow-1"></v-divider>
                <span class="mx-2 text-center">or</span>
                <v-divider class="flex-grow-1"></v-divider>
              </div>

              <!-- Social Login -->
              <v-btn
                block
                color="blue darken-1"
                class="mb-2"
                height="45"
                prepend-icon="mdi-facebook"
                href="https://www.facebook.com"
              >
                Login with Facebook
              </v-btn>
              <v-btn
                block
                variant="outlined"
                color="grey"
                height="45"
                prepend-icon="mdi-google"
                href="https://accounts.google.com"
              >
                Login with Google
              </v-btn>

              <!-- Sign Up Link -->
              <div class="text-center mt-4">
                Don’t have an account?
                <RouterLink :to="{ name: 'register' }" class="text-blue text-decoration-none">
                  Sign Up
                </RouterLink>
                >
              </div>
            </v-form>
          </v-card>
        </v-container>
      </v-main>

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
