<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" justify="center">
      <Login />
    </v-row>
  </v-container>
</template>

<script>
import Login from '@/components/Login/Login.vue'

export default {
  components: {
    Login
  }
}
</script>
