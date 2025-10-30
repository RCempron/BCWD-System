<script setup>
import { useDisplay } from 'vuetify'
import { ref, watch } from 'vue'

const props = defineProps(['isDrawerVisible'])

// Utilize predefined vue functions
const { mobile } = useDisplay()

// Load Variables
const isDrawerVisible = ref(props.isDrawerVisible)
watch(props, () => {
  isDrawerVisible.value = props.isDrawerVisible
})

// Main Navigation
// bayloan pag icon
const mainNav = [
  ['Complaint History', 'mdi-account-box-multiple'],
  ['Notification', 'mdi-clipboard-list'],
  ['Settings', 'mdi-invoice-list'],
  ['Logout', 'mdi-cash-register'],
  ['Reporting', 'mdi-file-chart']
]
</script>

<template>
  <v-navigation-drawer
    v-model="isDrawerVisible"
    :temporary="mobile"
    :permanent="!mobile"
    width="350"
  >
    <v-list density="compact" nav>
      <v-list-item prepend-icon="mdi-view-dashboard" title="Home" value="Home"></v-list-item>

      <v-divider></v-divider>

      <v-divider></v-divider>

      <v-list-item
        prepend-icon="mdi-wrench"
        title="Complaint History"
        value="Complaint History"
      ></v-list-item>
      <v-list-item
        prepend-icon="mdi-wrench"
        title="Notification"
        value="Notification"
      ></v-list-item>
      <v-list-item prepend-icon="mdi-wrench" title="Settings" value="Settings"></v-list-item>
      <v-list-item prepend-icon="mdi-wrench" title="Logout" value="Logout"></v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>
