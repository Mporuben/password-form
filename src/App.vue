<template>
  <div id="app">
    <div class="card">
      <h2>Password Form</h2>
      <div class="formItem">
        <label>Password</label>
        <input v-model="password" :type="passwordType" />
      </div>
      <div class="formItem">
        <label>Password Confirmation</label>
        <input v-model="passwordConfirmation" :type="passwordType" />
      </div>
      <div>
        <button class="m-1" @click="togglePasswordVisibility">
          {{ (passwordVisibility) ? 'Hide password' : 'Show password' }}
        </button>
        <generate-password class="m-1" @generated="passwordGenerated" />
      </div>
      <div class="formItem">
        <button class="m-1">Submit</button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import GeneratePassword from './plugins/password/GeneratePassword.vue'

export default defineComponent({

  components: {
    GeneratePassword
  },

  data() { return {
    password: '',
    passwordConfirmation: '',
    passwordVisibility: false
  }},

  computed: {
    passwordType() {
      return this.passwordVisibility ? 'text': 'password'
    }
  },

  methods: {
    togglePasswordVisibility() {
      this.passwordVisibility = !this.passwordVisibility
    },

    passwordGenerated(pass: string) {
      this.password = pass
      this.passwordConfirmation = pass
      this.passwordVisibility = true
    },
  }

})
</script>

<style lang="sass" scoped>
#app
  text-align: center
  height: 100vh
  background: #222222
  display: flex
  justify-content: center
  align-items: center
  .card
    background: #111111
    padding: 10px 30px
    border-radius: 10px
    width: 260px
    color: white
    .formItem
      display: flex
      flex-direction: column
      align-items: stretch
      justify-content: stretch
      text-align: left
      margin: 10px 0px
</style>
