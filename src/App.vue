<template>
  <div>
    <div>

      <input placeholder="test"/>
      <input placeholder="test"/>

      <GeneratePassword />

      <button>Odoslat</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import GeneratePassword from './plugins/password/GeneratePassword.vue'

export default defineComponent({
  name: 'App',
  components: {
    GeneratePassword
  }


})
</script>

<style lang="sass">
#app
  font-family: Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  margin-top: 60px
</style>
