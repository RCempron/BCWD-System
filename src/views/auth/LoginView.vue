<script setup>
import AppLayout from '@/components/layout/AppLayout.vue'
import LoginForm from '@/components/auth/LoginForm.vue'
import { ref } from 'vue'
import { useRouter, RouterLink } from 'vue-router' // Import RouterLink

const icons = ['mdi-facebook', 'mdi-twitter', 'mdi-linkedin', 'mdi-instagram']
</script>

<template>
  <AppLayout>
    <template #content>
      <v-card class="pa-6" max-width="400" elevation="0">
        <!-- Title -->
        <div class="text-center mb-6">
          <h2 class="font-weight-bold">Hi, Welcome Back!</h2>
        </div>
        
        <LoginForm></LoginForm>
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
