<script setup>
import { ref } from 'vue'


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
      <RouterLink to="/dashboard">Login</RouterLink>
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
</template>
