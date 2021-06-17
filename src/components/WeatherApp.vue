
<template>
  <main class="container">
    <div class="search-block">
      <div class="input-search-block">
        <input
          type="search"
          name="q"
          id="search-input"
          placeholder="Type the city"
          v-model="cityname"
        />
        <a id="search-button"  v-on:click="getApi" >Search</a>
      </div>
      <div class="img-block">
        <img :src=img id="img" alt="" />
      </div>
      <div class="city-info">
        <h3>{{description}}</h3>
        <div class="temp">
          <h2 class="temp-text">
            <img
              src="https://i.imgur.com/GedNCpM.png"
              id="min-temp"
              alt=""
            />{{mintemp}}<span>ºF</span>
          </h2>
          <h1 class="temp-text">{{temp}}<span>ºF</span></h1>
          <h2 class="temp-text">
            {{maxtemp}}<span>ºF</span
            ><img src="https://i.imgur.com/w3XtFNR.png" id="max-temp" alt="" />
          </h2>
        </div>
        <div class="city">
          <h3>
            <span><img src="https://i.imgur.com/62NEawS.png" alt="" id="map-pin" /></span>
            {{city}}, {{country}}
          </h3>
          <h3>{{date}}</h3>
        </div>
      </div>
    </div>



    <div class="info-block">
        <div class="weather-search">
            <h1>Weathersearch</h1>
        </div>

        <div id="highlights">
            <h1>Today´s highlights</h1>
        </div>


      <div class="container-info">
        <div class="block-info">
            <div class="block">

                <h1 class="title">Wind <img class="img-icon" src="https://i.imgur.com/QHARDOL.png" alt=""></h1>
                <div class="info">
                <h2 >{{wind}}<span>km/h</span></h2>
                </div>
                    
            </div>
        </div>

        <div class="block-info">

            <div class="block">

                <h1 class="title">Pressure <img  class="img-icon" src="https://i.imgur.com/Zu2Cowd.png" alt=""></h1>
                <div class="info">
                <h2 >{{pressure}}<span>mb</span></h2>
                </div>
                    

            </div>
        </div>

        <div class="block-info">

                <div class="block">

                    <h1 class="title">Real Feel  <img class="img-icon" src="https://i.imgur.com/ryG26xI.png" alt=""></h1>

                    <div class="info">
                <h2 >{{realfeel}}<span>ºF</span></h2>
                </div>
                    
            </div>
        </div>

        <div class="block-info">

            <div class="block">

                <h1 class="title">Humidity <img class="img-icon" src="https://i.imgur.com/vND2HLX.png" alt=""></h1>
                <div class="info">
                 <h2>{{humidity}}<span>%</span></h2>
                </div>
    
            </div>

        </div>

      </div>


    </div>
  </main>
</template>


<script>
import axios from 'axios';
export default {
    name: 'container',
    props: [],
    data(){
      return {
        city: '',
        mintemp: '',
        maxtemp: '',
        temp: '',
        description: '',
        cityname: '',
        wind: '',
        pressure: '',
        realfeel: '',
        humidity: '',
        date: '',
        country: '',
        img: ''
        
        
    }

    },
    methods: {

      kevinToFahr(temp){
        let fahr = 0
        fahr = (1.8 * (temp-273) + 32).toFixed(0)
        return fahr
      },
     
      async getApi(){ 
        let city = this.cityname
        
        try {
          const {data} = await axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=c26c9e9ea4b6fca5b999348eed7781af`)
        .then(response => response);
        this.putInfo(data)
        console.log();
       // data.weather[0].id
        
        
        } catch (error) {
          alert("City not found!")
          this.cityname = ''
        }

      },


      setImg(id_desc){
        const imgs = {
          clearsky: 'https://i.imgur.com/GMfd8H8.png',
          lightrain: 'https://i.imgur.com/Z4qQzKb.png',
          broken: 'https://i.imgur.com/BgYJmir.png',
          overcast: 'https://i.imgur.com/zMrXcSH.png',
          scattered: 'https://i.imgur.com/BgYJmir.png',
          fewclouds: 'https://i.imgur.com/XQPohpT.png'
        }


        switch (id_desc) {
          case 800:
            this.img = imgs.clearsky
     
            break;

             case 801:

            this.img = imgs.fewclouds

            break;

             case 802:

            this.img = imgs.scattered

            break;

             case 803:

            this.img = imgs.broken

            break;

             case 804:

            this.img = imgs.overcast

               break;

             case 500:

            this.img = imgs.lightrain

            break;
        }
       

      },

        putInfo(data){
        this.maxtemp = this.kevinToFahr(data.main.temp_max) 
        this.mintemp = this.kevinToFahr(data.main.temp_min)  
        this.temp = this.kevinToFahr(data.main.temp)
        this.city = data.name
        this.country = data.sys.country
        this.description = data.weather[0].description


        this.wind = (data.wind.speed * 3.6).toFixed(1)
        this.pressure = data.main.pressure
        this.humidity = data.main.humidity
        this.realfeel = this.kevinToFahr(data.main.feels_like)


        var datas = new Date;
        this.date = datas.toDateString()


        this.setImg(data.weather[0].id)

      },


    }

};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300;400&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700;900&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "roboto", sans-serif;
  color: rgb(240, 240, 240);
}

.container {
  background-color: rgb(0, 53, 78);;
  width: 100vw;
  height: 100vh;
  display: grid;
  grid-template-columns: 2.3fr 5fr;
}

.search-block {
  background-color: rgba(39, 86, 107, 0.61); /* 218 218 218*/
 
}

.info-block {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.block-info {
      display: flex;
    justify-content: center;
    align-items: center;
  width: 100%;
  background-color: rgba(39, 86, 107, 0.61);
   border-radius: 15px;

   box-shadow: 10px 11px 12px -6px rgb(32, 59, 78);
}

.info{
    padding-top: 45px;
    height: 100%;
    font-size: 3rem;
    display: flex;
    justify-content:flex-end;
    align-items: center;
}


.info span{
    font-size: 2rem;
}

.title{
    font-size: 1.4rem;
    text-align: left;
    color: rgb(218, 218, 218)
}

.block{
    width: 90%;
    height: 80%;
    color: rgb(218, 218, 218)
}

.weather-search{
    font-size: 2.5rem;
    padding: 1rem;
    color: rgb(218, 218, 218);
    letter-spacing: 3px;
    text-shadow: 2px 3px rgb(122, 122, 122);
}

#highlights{
    font-size: 0.8rem;
    width: 90%;
    padding: 7px;
    color: rgb(218, 218, 218);
    text-shadow: 2px 1px rgb(88, 88, 88);
}

.container-info {
  width: 90%;
  height: 70%;
  display: grid;
  justify-content: center;
  grid-template-columns: 2fr 2fr;
  gap: 10px;
  
}

.input-search-block {
  width: 100%;
  height: 15%;
  display: flex;
  justify-content: center;
  align-items: center;
}

#search-input {
  width: 70%;
  height: 30%;
  background-color: rgba(245, 245, 245, 0.205);
  outline: none;
  padding: 0px 10px;
  border-radius: 5px;
  font-size: 0.9rem;
  border: none;
  
}

#search-input::-webkit-search-cancel-button{
    position: relative;
  -webkit-appearance:none;
}


#search-input::placeholder{
    color: rgb(199, 199, 199);
}

#search-button {
  width: 20%;
  height: 30%;
  font-size: 0.9rem;
  text-align: center;
  background-color: rgb(4, 50, 80);
  margin-left: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  border-radius: 5px;
  border-bottom: 2px solid black;
  color: rgb(255, 255, 255);
  font-weight: bold;
  letter-spacing: 1px;
}

.img-block {
  width: 100%;
  height: 30%;
  display: flex;
  justify-content: center;
  align-items: center;
}

#img {
  width: 30%;
  height: auto;
  background-size: cover;
}

.city-info {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: auto;
}


.city-info h3{
  text-transform: capitalize;
  text-align: center;
}

.temp {
  display: flex;
  margin-top: 50px;
}

.temp h1 {
  margin: 25px;
}

#min-temp {
  transform: rotate(180deg);
}

.city {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  margin-top: 22%;
}

#map-pin {
  width: 170px;
  max-width: 8%;
  height: auto;
  background-size: cover;
}

.temp-text {
  font-size: 3rem;
  font-family: "Nunito", sans-serif;
}

span {
  font-size: 0.9rem;
  font-family: "Nunito", sans-serif;
}

.img-icon{
    max-width: 30px;
    width: 6%;
    height: auto;
    background-size: cover;
}



.city{
  bottom: 5%;
  position: absolute;
  
}
</style>
