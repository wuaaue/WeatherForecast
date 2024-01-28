<template>
  <div class="wrapper">
    <h1>Weather</h1>
    <p>Find out the weather in {{city == "" ? "your city" : cityName}} </p>
    <input type="text" v-model="city" placeholder="Enter city">
    <button v-show="city != '' " @click="getWeather()">Get weather</button>
    <p class="error">{{error}}</p>

    <div v-if="info != null" >
      <p>{{showTemp}}</p>
      <p>{{showFeelsLike}}</p>
      <p>{{showMinTemp}}</p>
      <p>{{showMaxTemp}}</p>
    </div>

  </div>
</template>

<script >
import axios from 'axios'
export default {
  data(){
    return{
      city:"",
      error:"",
      info: null
    }
  },
  computed:{
    cityName(){
      return " ' " + this.city + " ' "
    },
    showTemp(){
      return "Temperature: " + Math.round(this.y.main.temp)
    },
    showFeelsLike(){
      return "Feels Like: " + Math.round(this.info.main.feels_like)
    },
    showMinTemp(){
      return "Min temperature:" + Math.round(this.info.main.temp_min)
    },
    showMaxTemp(){
      return "Max temperature:" + Math.round(this.info.main.temp_max)
    },
  },
  methods:{
    getWeather(){
      if(this.city.trim().length<2){
        this.error="Need more than one character name ;)"
        return false
      }
      this.error = ""

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=0a0afac2c0622feac524d684fed2700b`)
         .then(res =>(this.info = res.data))
    }
    }
}
</script>

<style scoped>
.error{color: brown}
.wrapper{
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #000000;
  text-align: center;
  color: #b26cf8;
}

.wrapper h1{
  margin-top: 50px;
}
.wrapper p{
  margin-top: 20px;
}
.wrapper input {
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #b26cf8;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
  color: #b26cf8 ;
}
.wrapper input:focus{
  border-bottom-color: aqua;
}
.wrapper button{
  background: #291636;
  color: #b26cf8;
  border-radius: 10px;
  border: 2px solid #b26cf8;
  padding: 10px 15px;
  margin-left:20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}

</style>
