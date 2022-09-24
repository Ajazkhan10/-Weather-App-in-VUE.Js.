<template>
  <div class="all-top">
    <div class="section" v-for="current in weather" :key="current">
      <h1>Weather App</h1>
      <div class="main">
       <div class="inputData">
        <input class="input"
          type="text"
          placeholder="Search city"
          v-model.trim="query"
        />
       <button @click="getweather()"><i class="fa fa-search" aria-hidden="true"></i></button>
       </div>

        <!-- <h3>Thuesday 5 December 8:42 am</h3> -->
        <h3>{{current.location.country}} {{current.location.localtime}}  {{current.location.region}} {{current.location.tz_id}}</h3>
        <div class="screen"> {{current.current.temp_c}}°C {{current.current.temp_f}} °F</div>
        <h3>{{current.current.cloud}} %  Cloud</h3>
        <h3>{{current.current.condition.text}} </h3>
        <!-- <p>{{current.current.condition.icon}}</p> -->
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      query: "delhi",
      weather: [],
    };
  },
  mounted(){
      this.getweather()
  },
  methods: {
 getweather() {
        axios.get(
          `https://api.weatherapi.com/v1/current.json?key=f0c7371671fb4de7842101244222409&q=${this.query}&aqi=no`
        )
        .then((response) => {
          this.weather.push(response.data);
          console.log(response);
        })
        .catch((err) => {
          console.log(err);
        });
    }}
};
</script>
<style scoped>
.all-top {
  width: 100%;
  height: 100vh;
  background: rgb(129, 245, 226);
  background-image: url("../assets/4924abfb01a49999d109d21742fe4b80.jpg");
  background-size:100% 100vh;
  background-position: center;
  background-repeat: no-repeat;
  text-align: center;
  justify-content: center;
  display: flex;
}
.section {
  width: 25%;
  position:fixed;
  top: 0;
  bottom: 0;
  text-align: center;
  display: flex;
  background-image: url("../assets/4924abfb01a49999d109d21742fe4b80.jpg");
  background-size:100% 100vh;
  background-position: center;
  background-repeat: no-repeat;  flex-direction: column;
  justify-content: center;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px,
    rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px,
    rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
  margin: 10px;
  border-radius: 35px;
}
.section h1 {
  width: 90%;
  height: 50px;
  padding: 10px;
  color: rgb(211, 211, 211);
  font-size: 40px;
  font-weight: 700;
  font-family: "Times New Roman", Times, serif;
}
.main {
  width: 100%;
  height: 70vh;
  display: inline-flex;
  flex-direction: column;
}

.main h3 {
  margin-top: 30px;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 20px;
  font-weight: 700;

  color: rgb(255, 255, 255);
}
.screen {
  margin: 20px auto;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  font-size: 45px;
  font-weight: 600;
  width: 200px;
  height: 100px;
  color: aliceblue;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 10px 50px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 20px;
}
.inputData{
  width: 100%;
  height: 30px;
  display: inline-flex;
  text-align: center;
  justify-content: center;
}
.inputData .input{
  width: 70%;
  padding-left: 20px;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 12px;
  border: none;
  border-radius: 20px;
  color: black;
  background: rgb(211, 211, 211);
}
.inputData button{
  width: 10%;
  border-radius: 50px 50px;
  border: none;
  margin-left: 10px;
  cursor: pointer;
  background: rgb(211, 211, 211);
}
.inputData button:hover{
  background: white;
  color: black;
}
</style>