<template>
  <v-card width="320">
    <!-- <v-app-bar dark color="primary">
      <span>Login</span>
    </v-app-bar> -->
    <v-card-text>
      <v-text-field small label="Login" outlined></v-text-field>
      <v-text-field small label="Password" outlined type="password"></v-text-field>
      <v-btn block color="primary" class="white--text">
        LOGIN
      </v-btn>
    </v-card-text>
  </v-card>
</template>
<script>

export default {
  name: 'Login',
  components: {},
  data: () => ({

  })

}
</script>

<style lang="sass" scoped>


</style>
