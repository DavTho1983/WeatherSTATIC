<template>
  <div class="container">
    <div>
      <h1>London Weather</h1>
      <div id="example-1"></div>
      <button @click="plus()">
        <font-awesome-icon :icon="['fas', 'plus']"/>
      </button>
      <button @click="minus()">
        <font-awesome-icon :icon="['fas', 'minus']"/>
      </button>
    </div>
    <div class="row">
      <div class="column1">
        <div>
          <p>This is record {{data.id}}</p>
        </div>
        <p>DATETIME: {{data.datetime}}</p>
        <p>LONGITUDE: {{data.longitude}}</p>
        <p>LATITUDE: {{data.latitude}}</p>
        <p>MAIN WEATHER: {{data.main_weather}}</p>
        <p>DESCRIPTION: {{data.description}}</p>
        <p>TEMPERATURE: {{data.temperature}}</p>
        <p>PRESSURE: {{data.pressure}}</p>
        <p>HUMIDITY: {{data.humidity}}</p>
        <p>MIN TEMPERATURE: {{data.min_temp}}</p>
        <p>MAX TEMPERATURE: {{data.max_temp}}</p>
        <p>WIND SPEED: {{data.wind_speed}}</p>
        <p>WIND DIRECTION: {{data.wind_direction}}</p>
        <p>CLOUDS: {{data.clouds}}</p>
      </div>
      <div class="column2">
        <img src="~/static/London.jpg">
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  head() {
    return {
      title: 'Weather'
    }
  },
  data: function() {
    return { counter: 1 }
  },
  methods: {
    plus: function(counter, data, datalength) {
      this.counter += 1
      axios.get('http://localhost:8000/api/' + this.counter).then(res => {
        console.log(this.counter)
        console.log(res.data)
        return (this.data = res.data)
      })
    },
    minus: function(counter, data) {
      if (this.counter >= 2) {
        this.counter -= 1
        axios.get('http://localhost:8000/api/' + this.counter).then(res => {
          console.log(this.counter)
          console.log(res.data)
          return (this.data = res.data)
        })
      } else {
        this.counter = 1
      }
    }
  },
  async asyncData({ params, counter }) {
    let { data } = await axios.get('http://localhost:8000/api/1')
    return { data }
  }
}
</script>