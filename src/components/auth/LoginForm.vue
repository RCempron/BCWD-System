<script setup>
import { requiredValidator, emailValidator } from '@/utils/validators'
import { ref } from 'vue'

const isPasswordVisible = ref(false)
const refVForm = ref()

const formDataDefault = {
  email: '',
  password: '',
}

const formData = ref({
  ...formDataDefault,
})


const onSubmit = () => {
  // alert(formData.value.email)
}

const onFormSubmit = () => {
  refVForm.value?.validate().then(({ valid }) => {
    if (valid) onSubmit()
  })
}
</script>
<template>
  <!-- Login Form -->
  <v-form ref="refVForm" @submit.prevent="onFormSubmit">
    <!-- Email -->
    <v-text-field
      v-model="formData.email"
      label="Email"
      type="email"
      placeholder="example@gmail.com"
      outlined
      dense
      class="mb-3"
      :rules="[requiredValidator, emailValidator]"
    />

    <!-- Password -->
    <v-text-field
      v-model="formData.password"
      :type="isPasswordVisible ? 'text' : 'password'"
      label="Password"
      placeholder="Enter Your Password"
      outlined
      dense
      class="mb-2"
      :append-inner-icon="isPasswordVisible ? 'mdi-eye-off' : 'mdi-eye'"
      @click:append-inner="isPasswordVisible = !isPasswordVisible"
      :rules="[requiredValidator]"
    />

    <!-- Remember Me + Forgot Password -->
    <!-- <div class="d-flex justify-space-between align-center mb-4 text-small">
      <v-checkbox v-model="rememberMe" hide-details density="compact" class="text-small">
        <template #label>
          <span class="text-small">Remember Me</span>
        </template>
      </v-checkbox>
      <a href="#" class="text-red text-decoration-none">Forgot Password?</a>
    </div> -->

    <!-- Login Button -->
    <v-btn block color="primary" class="mb-4" height="45" type="submit">
      <!-- <RouterLink to="/dashboard">Login</RouterLink> -->Login
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
      
    </div>
  </v-form>
</template>
