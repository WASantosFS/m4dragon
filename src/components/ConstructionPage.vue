<template>
  <div>
    <h1>{{msg}}</h1>
    <p>{{getClientIP()}}</p>
    <p>{{getWeatherReport()}}</p>
    <div>
      <p>Pardon the dust as we make things made!</p>
      <p>To keep you entertained while you wait for dust to settle, here is a random <a :href="randomUrl()">Project Euler problem</a>!</p>
    </div>
    <h2>For your own information... here's your weather!</h2>
    <p id="subtitle">(Because... you know... that's what you do when you're bored. Right? ...no? Just me then? Okay...)</p>
    <div id="tableDiv">
      <table>
        <th>Your Weather</th>
        <tr>
          <td>Temperature: {{weatherReport.currentTemp}}F</td>
        </tr>
        <tr>
          <td>Precipitation: {{weatherReport.precip}} inches</td>
        </tr>
        <tr>
          <td>Humidity: {{weatherReport.humidityPer}}%</td>
        </tr>
        <tr>
          <td>Pressure: {{weatherReport.pressure}} inches</td>
        </tr>
        <tr>
          <td>Wind Speed: {{weatherReport.windSpeed}}mph</td>
        </tr>
        <tr>
          <td>Wind Degree: {{weatherReport.windDegree}}deg</td>
        </tr>
        <tr>
          <td>UV Rating: {{weatherReport.uvNum}}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "ConstructionPage",
  props: {
    msg: String,
  },
  data() {
    return {
      weatherReport: {
        clientIP: "",
        currentTemp: "32",
        windSpeed: "21",
        windDegree: "42",
        pressure: "23",
        precip: "0.0",
        humidityPer: "65.4",
        uvNum: "0.0",
      },
    }
  },
  methods: {
    randomUrl() {
      let rand = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;
      return "https://projecteuler.net/problem=" + rand(1, 734);
    },
    getClientIP() {
      let report = this.weatherReport;
      axios.get('https://api.ipify.org?format=json')
          .then(function (response) {
            //console.log(response.data);
            report.clientIP = response.data.ip;
            //console.log("hello " + ip);
          })
          .catch(function (error) {
            console.log(error);
          });

    },
    getWeatherReport() {
      let report = this.weatherReport;
      const baseUrl = "https://api.weatherapi.com/v1/current.json?key=2568f3eea4c2454eb9f224333200911&q=";
      const joinedUrl = baseUrl + report.clientIP;
      axios.get(joinedUrl)
          .then(function (response) {
            report.currentTemp = response.data.current.temp_f;
            report.windSpeed = response.data.current.wind_mph;
            report.windDegree = response.data.current.wind_degree;
            report.pressure = response.data.current.pressure_in;
            report.precip = response.data.current.precip_in;
            report.humidityPer = response.data.current.humidity;
            report.uvNum = response.data.current.uv;
            //console.log(response.data);
          })
          .catch(function (error) {
            console.log(error);
          });
    }
  }
}
</script>

<style scoped>
p {
  font-size: 20px;
}
#subtitle {
  font-size: 14px;
}
table {
  margin: 0 auto;
  border: 3px solid darkslategrey;
  border-radius: 7px;
}
th {
  border-bottom: 3px solid darkslategrey;
}
tr {
  text-align: left;
}
</style>