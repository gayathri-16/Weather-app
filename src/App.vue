
<template>
  <div id="app " :class="typeof weather.main !='undefined' && weather.main.temp > 16 ? 'sun': ''">
    <div id="load">
    <main>
      <link rel="preconnect" href="https://fonts.gstatic.com">
      <link href="https://fonts.googleapis.com/css2?family=Castoro:ital@1&display=swap" rel="stylesheet"> 
      <link href="//maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet">
      <div class="search-box">
        <input 
        type="text"  
        class="search-bar" 
        placeholder="Search..." 
        v-model="query"
        @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }} </div>
            <div class="date"> {{dateBuilder()}} </div>
      </div>

      <div class="weather-box">
        <div class="temp"> {{ Math.round(weather.main.temp) }} <sup>o</sup>c</div>
          <div class="weather"> {{weather.weather[0] .main }} </div>
      </div>
          
      </div>
    </main>
  </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      api_key:'25473f353e7c959aeb1bf093f8cc8154',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{}
    }
  },
  methods:{
       fetchWeather(e){
         if(e.key == "Enter"){
           fetch( `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
           .then(res => {
             return res.json();
           }).then(this.setResults);
           }
         },
         setResults (results) {
               this.weather = results;
         },
         dateBuilder(){
           let d = new Date();
           let months = ["January", "February", "March", "April", "May", "June", "July", "August",
           "September", "October", "November", "December"];
           let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thurseday", "Friday", "Saturday"];

           let day = days[d.getDay()];
           let date = d.getDate();
           let month = months[d.getMonth()];
           let year = d.getFullYear();
            
            return `${day} ${date} ${month} ${year}`;
         }
  }

}
</script>

<style>

body{
  font-family: 'Castoro', serif;
}
#app{
  background-image: url('./assets/cold.jpg');
  background-position: bottom;
  width: 200%;
  height: 100vh;
  transform: translate(-50%,-50%);
  animation-delay:0s;
  
}

#load{
  animation: slide 100s infinite;
  
}
@keyframes slide{
       0%{
         background-image: url('./assets/dark.jpg');
       }
        20%{
         background-image: url('./assets/fall.jpg');
       }
        20.01%{
         background-image: url('./assets/ice.jpg');
       }
        40%{
         background-image: url('./assets/spring.jpg');
       }
        40.01%{
         background-image: url('./assets/red.jpg');
       }
        60%{
         background-image: url('./assets/tower.jpg');
       }
        60.01%{
         background-image: url('./assets/windy.jpg');
       }
        80%{
         background-image: url('./assets/rain.jpg');
       }
    20%{
         background-image: url('./assets/purple.jpg');
       }

}
main{
  min-height: 100vh;
padding:25px;
background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75) );
}
.search-box{
  width:100%;
  margin-bottom:30px;
}
.search-box .search-bar{
  display:block;
  width:50%;
  padding:15px;
  top:25%;
  margin-left:20%;
  color:#313131;
  font-size:20px;
  appearance: none;
  border: none;
  outline:none;
  background: none;
  border-radius: 0px 16px 0px 16px;

}
.search-box :focus{
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color:rgba(153, 147, 147, 0.75);
  border-radius:16px 0px 16px 0px;
}
.location-box .location{
  color:#FFF;
  font-size:30px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date{
  color:#FFF;
  font-size:20px;
  font-weight: 300;
  text-align: center;
  font-style:italic;
  }

  .weather-box{
    text-align:center;
  }

.weather-box .temp{
  display: inline-block;
  padding: 10px 30px;
  color:#FFF;
  font-size: 120px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin:30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);

}
.weather-box .weather{
  color:#eee;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);

}
</style>
