<template>
  <div style="display: flex;justify-content: center;">
    <div class="weatherContainer">
      <img :src="details.data.current.condition.icon" alt="">
    <h1>{{ details.data.location.name }}</h1>
    <p>{{ details.data.location.region }}</p>
    <h1 class="c">{{ details.data.current.temp_c }} c</h1>
    </div>
  </div>
  
</template>

<script>
import axios from 'axios';
export default {
  name: 'App',
  data(){
    return {
      details: {},
      inputCity: 'Nouakchot'
    }
  },
  async created(){
    await this.getData()
    await console.log(this.details);
  },
  methods: {
    async getData(){
      this.details = await axios.get(`https://api.weatherapi.com/v1/current.json?key=5dd8525ecc1844fe8d841715231309&q=${this.inputCity}&aqi=yes`).then((res)=> res).catch((e)=> e);
      this.details.data.current.temp_c = await parseInt(this.details.data.current.temp_c)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.c{
  font-size: 45px;
}
.weatherContainer{
  background: #eeeeee52;
  width: fit-content;
  padding: 8px 45px;
  border: 0px solid #2c3e50;
  border-radius: 8px;
}
</style>
