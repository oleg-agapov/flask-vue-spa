<template>
  <div>
    <p>Vue Home page example </p>
    <p>Random number are generated from backend by clicking button: {{ randomNumber }}</p>
    <button @click="getRandom">New random number</button>
    <b-table striped hover :items="items" />
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
      this.randomNumber = this.getRandomInt(1, 100)
      this.randomNumber = this.getRandomFromBackend()
    },
    getRandomFromBackend () {
      const path = `http://127.0.0.1:5000/api/random`
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
