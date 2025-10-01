<script setup>
import AppLayout from '@/components/layout/AppLayout.vue'
import RegisterForm from '@/components/auth/RegisterForm.vue'
import { useDisplay } from 'vuetify'

const { mobile } = useDisplay()
</script>

<template>
  <AppLayout>
    <template #content>
      <v-card class="pa-6" max-width="400" elevation="0">
        <!-- Title -->
        <div class="text-center mb-6">
          <h2 class="font-weight-bold">Create an account</h2>
        </div>

        <RegisterForm></RegisterForm>
      </v-card>
    </template>
  </AppLayout>
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
