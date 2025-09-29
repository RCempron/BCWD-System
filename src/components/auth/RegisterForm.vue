<script setup>
import { ref } from 'vue'

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
    <v-btn block color="primary" class="mb-4" height="45" @click="register"> Sign Up </v-btn>

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
</template>
