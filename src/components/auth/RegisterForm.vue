<script setup>
import {
  requiredValidator,
  emailValidator,
  passwordValidator,
  confirmedValidator,
} from '@/utils/validators'
import { ref } from 'vue'

const formDataDefault = {
  firstname: '',
  lastname: '',
  email: '',
  password: '',
  password_confirmation: '',
}

const formData = ref({
  ...formDataDefault,
})

const isPasswordVisible = ref(false)
const isPasswordConfirmVisible = ref(false)
const refVForm = ref()

const onSubmit = () => {
  alert(formData.value.email)
}

const onFormSubmit = () => {
  refVForm.value?.validate().then(({ valid }) => {
    if (valid) onSubmit()
  })
}
</script>

<template>
  <!-- Register Form -->
   
  <v-form ref="refVForm" @submit.prevent="onFormSubmit">
    <!-- Username -->
    <v-text-field
       v-model="formData.firstname"
      label="Firstname"
      placeholder="Enter Your Firstname"
      outlined
      dense
      class="mb-3"
      :rules="[requiredValidator]"
    />

    <!-- Email -->
    <v-text-field
      v-model="formData.email"
      label="Email"
      type="email"
      placeholder="Enter Your Email"
      outlined
      dense
      class="mb-3"
      :rules="[requiredValidator, emailValidator]"
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
      v-model="formData.password"
      :type="showPassword ? 'text' : 'password'"
      label="Password"
      placeholder="Enter Your Password"
      outlined
      dense
      class="mb-2"
      :append-inner-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'"
      @click:append-inner="showPassword = !showPassword"
      :rules="[requiredValidator, passwordValidator]"
    />

    <v-col cols="12" md="6">
      <v-text-field
        v-model="formData.password_confirmation"
        label="Password Confirmation"
        :type="isPasswordConfirmVisible ? 'text' : 'password'"
        :append-inner-icon="isPasswordConfirmVisible ? 'mdi-eye-off' : 'mdi-eye'"
        @click:append-inner="isPasswordConfirmVisible = !isPasswordConfirmVisible"
        :rules="[
          requiredValidator,
          confirmedValidator(formData.password_confirmation, formData.password),
        ]"
      ></v-text-field>
    </v-col>

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
      type="submit"
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
