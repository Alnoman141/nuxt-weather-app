<template>
  <div class="container">
    <div class="w-100">
      <h1 class="my-3 display-4">Weather App</h1>
      <b-card v-if="data.name" bg-variant="dark" text-variant="white" :title="`${data.name} Weather Info`" class="col-sm-12">
        <b-card-text>
          <b-row>
            <b-col sm="4">
              <h3>Temperature Info</h3>
              <b-row>
                <b-col sm="12">Temperature : {{ Math.round(data.main.temp - 273) }} &deg;C </b-col>
                <b-col sm="12">Max Temperature : {{ Math.round(data.main.temp_max - 273) }} &deg;C </b-col>
                <b-col sm="12">Min Temperature : {{ Math.round(data.main.temp_min - 273) }} &deg;C </b-col>
                 <b-col sm="12">Feels Like : {{ Math.round(data.main.feels_like - 273) }} &deg;C</b-col>
              </b-row>
            </b-col>
            <b-col sm="4">
              <h3>Basic Info</h3>
              <b-row>
                <b-col sm="12">Humidity : {{ data.main.humidity}} %</b-col>
                <b-col sm="12">Pressure : {{ data.main.pressure}} hPa</b-col>
                <b-col sm="12">Wind Speed : {{ data.wind.speed}} meter/sec</b-col>
              </b-row>
            </b-col>
            <b-col sm="4">
              <h3>Weather Info</h3>
              <b-row>
                <b-col sm="12">
                  <img :src="`http://openweathermap.org/img/wn/${data.weather[0].icon}.png`">
                </b-col>
                <b-col sm="12">Description : {{ data.weather[0].description}}</b-col>
              </b-row>
            </b-col>
          </b-row>
        </b-card-text>
      </b-card>
      <b-card bg-variant="dark" text-variant="white" class="mt-5 col-sm-12">
        <b-card-text>
          <b-form @submit.prevent="onSubmit" @reset="onReset" v-if="show">
            <b-form-group
              id="input-group-1"
              label="City Name:"
              label-for="city"
              description="Please Enter City Name"
            >
              <b-form-input
                id="city"
                v-model="city"
                type="text"
                placeholder="Please Enter City Name"
                required
              ></b-form-input>
            </b-form-group>
            <b-button type="submit" variant="primary">Submit</b-button>
          </b-form>
        </b-card-text>
      </b-card>

    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      show: true,
      city: '',
      appID: '6cea3162b2b071b2574f8440d8268861',
      appURL: 'https://api.openweathermap.org/data/2.5/weather',
      data: {}
    }
  },
  created(){

  },
  methods: {
    onSubmit(){
      this.$axios.$get(`${this.appURL}?q=${this.city}&appid=${this.appID}`).then(response => {
        this.data = response;
        console.log(this.city);
      })
    },
    onReset(){

    }
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  /* align-items: center; */
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
