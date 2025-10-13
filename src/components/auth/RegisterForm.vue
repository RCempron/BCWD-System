<script setup>
import {
  requiredValidator,
  emailValidator,
  passwordValidator,
  confirmedValidator,
} from '@/utils/validators'
import { ref } from 'vue'
import AlertNotification from '@/components/common/AlertNotification.vue'
import { supabase, formActionDefault } from '@/utils/supabase.js'

const formDataDefault = {
  firstname: '',
  lastname: '',
  email: '',
  password: '',
  phone: '',
  password_confirmation: '',
}

const formData = ref({
  ...formDataDefault,
})

const formAction = ref({
  ...formActionDefault,
})

const isPasswordVisible = ref(false)
const isPasswordConfirmVisible = ref(false)
const refVForm = ref()

const onSubmit = async () => {
  formAction.value = { ...formActionDefault } //para ma reset ang error na message kung mag invalid
  formAction.value.formProcess = true

  const { data, error } = await supabase.auth.signUp({
    email: formData.value.email,
    password: formData.value.password,
    options: {
      data: {
        firstname: formData.value.firstname,
      },
    },
  })
  //kung naay error
  if (error) {
    console.log(error)
    formAction.value.formErrorMessage = error.message
    formAction.value.formStatus = error.status
  } else if (data) {
    //kung walay errror
    console.log(data)
    formAction.value.formSuccessMessage = 'Successfully Registered Account.'
    // Add here more actions if you want
    refVForm.value?.reset()
  }

  formAction.value.formProcess = false
}

const onFormSubmit = () => {
  refVForm.value?.validate().then(({ valid }) => {
    if (valid) onSubmit()
  })
}
</script>

<template>
  <AlertNotification
    :form-success-message="formAction.formSuccessMessage"
    :form-error-message="formAction.formErrorMessage"
  ></AlertNotification>

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
      v-model="formData.phone"
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
      :type="isPasswordVisible ? 'text' : 'password'"
      label="Password"
      placeholder="Enter Your Password"
      outlined
      dense
      class="mb-2"
      :append-inner-icon="isPasswordVisible ? 'mdi-eye-off' : 'mdi-eye'"
      @click:append-inner="isPasswordVisible = !isPasswordVisible"
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
    <v-btn
      block
      color="primary"
      class="mb-4"
      height="45"
      type="submit"
      :disabled="formAction.formProcess"
      :loading="formAction.formProcess"
    >
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
