<template>
  <div id="app" :class="typeof weather.main !== 'undefined' ? 'warm' : ''">
    <div>
      <main>
        <div class="search-box">
          <input
            type="text"
            placeholder="search"
            class="search-bar"
            v-model="query"
            @keypress="fet"
          />
        </div>

        <div class="box" v-if="typeof weather.main !== 'undefined'">
          <div class="location-box">
            <div class="location">
              {{ weather.sys.country }} : {{ weather.name }}
            </div>
            <div class="date">{{ getdate() }}</div>
          </div>

          <div class="weather-box">
            <div class="tem">
              {{ Math.floor(weather.main.temp - 272.15) }} c
            </div>
            <div class="weather">{{ weather.weather[0].main }}</div>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      weather: {},
      query: "",
      ap: "http://api.openweathermap.org/data/2.5/",
      apikey: "6c1216026d4897d4be44c5d98410dac1",
    };
  },
  //http://api.openweathermap.org/data/2.5/weather?q=paris&appid=6c1216026d4897d4be44c5d98410dac1
  methods: {
    fet(e) {
      //console.log(e)
      if (e.keyCode == "13") {
        fetch(`${this.ap}weather?q=${this.query}&appid=${this.apikey}`)
          .then((response) => response.json())
          .then((data) => {
            console.log(data);
            this.weather = data;
          });
      }
    },

    getdate() {
      let d = new Date();
      let date = d.getDate();
      let month = d.getMonth();
      let year = d.getFullYear();
      return `${date}/0${month + 1}/${year}`;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  width: 100%;
  height: 657px;
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
  background-image: url("73b150dd34a14ea9a85b00f263c5f997.jpeg");
  background-repeat: no-repeat;
  background-size: cover;
}

#app.warm {
  background-image: url("istock-1152164476.jpg");
}


.search-box {
  width: 100%;

  margin-bottom: 30px;

}
.search-box .search-bar {
  display: block;
  width: 98%;
  padding: 15px;
  font-size: 20px;
  color: rgb(78, 25, 36);
  background-color: rgb(203, 223, 208);

  margin-left: auto;
  margin-right: auto;
  border-radius: 8px;
}
.location-box {
  color: azure;
  text-align: center;
  width: 25%;
  margin: auto;
  height: 100%;
  margin-left: 400px;
}
.location-box .location {
  background-color: rgb(30, 100, 41);
  font-weight: bolder;
  font-size: 45px;
  border-radius: 8px;
  padding-top: 10px;
  height: 80px;
}
.location-box .date {
  background-color: rgb(49, 48, 73);
  font-size: 25px;
  border-radius: 8px;
  font-style: italic;
  height: 38px;
}

.weather-box {
  color: azure;
  text-align: center;
  width: 25%;
  margin: auto;
  margin-top: 20px;
  height: 100%;

  margin-left: 400px;
}
.weather-box .tem {
  background-color: rgb(6, 68, 34);
  font-weight: bolder;
  font-size: 70px;
  border-radius: 8px;
  height: 100px;
  padding: auto;
  text-align: center;
}
.weather-box .weather {
  background-color: rgb(17, 45, 58);
  font-weight: bolder;
  font-size: 35px;
  border-radius: 8px;
  height: 60px;
  padding-top: 7px;
  padding: auto;
  font-style: oblique;
}

</style>
