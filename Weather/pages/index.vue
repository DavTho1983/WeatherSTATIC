<template>
  <div class="container">
    <h1>London Weather</h1>
    <ul>
      <li v-for="record in data">{{ record }}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData({ params }) {
    // We can use async/await ES6 feature
    const { data } = await axios.get(`http://localhost:8000/api`)
    return { data }
  }
}
</script>
