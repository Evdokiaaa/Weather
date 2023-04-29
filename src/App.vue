<script>
export default {
    data(){
      return{
        API_KEY:'YOUR API KEY',
        URL:'https://api.openweathermap.org/data/2.5/',
        req:'',
        weather:{}
      }
  },
  methods: {
      async fetchWeather(e){
        if(e.key==='Enter'){
          await fetch(`${this.URL}weather?q=${this.req}&units=metric&APPID=${this.API_KEY}`)
              .then(res=>{
                return res.json();
              }).then(this.setResults)
        }
    },
    setResults(results){
        this.weather=results
    },
    showDate(){
      const today = new Date();
      const date = today.getFullYear() + '-' + (today.getMonth()+1) + '-' + today.getDate();
      return date

    }
  }
}
</script>

<template>
  <div class="content">
    <main class = 'main'>
      <div class="search__box">
        <input type="text"
               class = 'search__bar'
               placeholder="Search.."
               v-model="req"
               @keypress='fetchWeather'>

      </div>


    <div class="weather__content" v-if="typeof  weather.main!='undefined'">
     <div class="location__container">
       <div class="location">{{weather.name}}</div>
       <div class="date">{{showDate()}}</div>
     </div>
      <div class="weather__container">
        <div class="temperature">{{Math.round(weather.main.temp)}}</div>
        <div class="weather">{{weather.weather[0].main}}</div>
      </div>
    </div>
    </main>
  </div>

</template>

<style >

  @import url('https://fonts.googleapis.com/css2?family=Montserrat&display=swap');
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body{
    font-family: 'Montserrat',sans-serif;
  }
  .content{
    background-image: url('./assets/bg.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.5s;
  }

  .main{
    min-height: 100vh;
    padding: 20px;
    background-image: linear-gradient(to bottom, rgba(0,0,0,0.25),rgba(0,0,0,0.25))
  }

  .search__bar,
  .search__box{
    width: 100%;
    margin-bottom: 30px;
    padding: 15px;
    text-align: center;


    outline: none;
    border: none;
    appearance: none;


    font-size: 20px;
    border-radius: 10px;


  }


  .search__bar::placeholder{
    text-align: center;

  }

  .location{
    color:#FFF;
    font-size: 48px;
    font-weight: 500;
    text-align: center;

  }
  .date{
    color:#FFF;
    font-size: 24px;
    font-weight: 300;
    margin-top: 20px;
    text-align: center;

  }

  .weather__container{
    text-align: center;
  }
  .temperature{
    display: inline-block;
    color:#FFF;
    font-size: 5em;
    font-weight: 900;
    margin-top: 30px;
    padding: 10px 25px;
    background-color: rgba(255,255,255,0.25);
    text-shadow: 3px 5px rgba(0,0,0,0.25);
    border-radius: 15px;
    box-shadow: 3px 6px rgba(0,0,0,0.25);


  }
   .weather{
     color:#FFF;
     font-size: 48px;
     font-weight: 700;
     font-style: italic;
     text-shadow: 3px 5px rgba(0,0,0,0.25);
     margin-top: 30px;

   }







</style>
