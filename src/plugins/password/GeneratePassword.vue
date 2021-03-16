<template>
  <button @click="myGeneratePassword">{{title}}</button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import generator from 'generate-password'

export default defineComponent({

  //Moznosti konfiguracie generovaneho hesla
  props: {
    title: {
      default: 'Generate password',
      type: String
    },
    lowercase: {
      default: true,
      type: Boolean
    },
    uppercase: {
      default: true,
      type: Boolean
    },
    symbols: {
      default: true,
      type: Boolean
    },
    numbers: {
      default: true,
      type: Boolean
    },
    length: {
      default: 10,
      type: Number
    }
  },

  mounted() {
    if(!this.symbols && !this.lowercase && !this.uppercase && !this.numbers){
      console.error('You have to enable at least one character set')
    }
    if(this.length <= 0) {
      console.error('length has to be more then 0')
    }
  },

  methods: {

    //nevedel som ci na generovanie samotne mozem pouzit libku ak ano tak by som to vyriesil takto
    generatePassword() {
      const password = generator.generate({
        length: this.length,
        numbers: this.numbers,
        symbols: this.symbols,
        uppercase: this.uppercase,
        lowercase: this.lowercase
      })
      this.$emit('generated', password)
    },

    //ak si mam napisat vlastnu funkciu na generovanie tak by vyzerala takto
    myGeneratePassword() {
      const characters = this._getPasswordCharacters()
      let password = ''
      for(let i = 0; i < this.length; i++) {
        const randomIndex = Math.floor(Math.random() * Math.floor(characters.length))
        password += characters[randomIndex]
      }
      this.$emit('generated', password)
    },


    _getPasswordCharacters() {
      let par = ''
      par += this.symbols ? '!@#$%^&*()_+{}:"<>?\|[];\',./`~' : ''
      par += this.lowercase ? 'abcdefghijklmnopqrstuvwxyz' : ''
      par += this.uppercase ? 'ABCDEFGHIJKLMNOPQRSTUVWXYZ': ''
      par += this.numbers ? '0123456789' : ''
      return par
    }
  }
})

</script>
