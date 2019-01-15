<template>
  <div>
    <h1 style="color: gray;">Home page</h1>
    <router-link to="/About"><button style="width: 100px; height: 50px;">ABOUT</button></router-link>
    <p>Random number from backend: {{ randomNumber }}</p>
    <button @click="getRandom">New random number</button>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  data () {
    return {
      randomNumber: 0
    }
  },
  methods: {
    getRandomInt (min, max) {
      min = Math.ceil(min)
      max = Math.floor(max)
      return Math.floor(Math.random() * (max - min + 1)) + min
    },
    getRandom () {
      this.randomNumber = this.getRandomFromBackend(1, 100)
      // this.randomNumber = this.getRandomInt(1, 100)
    },
    getRandomFromBackend () {
      const path = `http://localhost:5000/api/random`
      axios.get(path)
        .then(response => {
          this.randomNumber = response.data.randomNumber
        })
        .catch(error => {
          console.log(error)
        })
    }
  },
  created () {
    this.getRandom()
  }
}
</script>
