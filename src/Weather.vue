<template>
  <section>
    <main id="weather">
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="Search..."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-list">
        <div class="weather-wrap" v-for="weather in weatherList" :key="weather.id">
          <div v-if="typeof weather.main != 'undefined'"
               :class="getClassWeather(weather)">
            <div class="location-box">
              <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
              <div class="date">{{ dateBuilder() }}</div>
            </div>

            <div class="weather-box">
              <div class="temp">{{ Math.round(weather.main.temp) }}&deg;c</div>
              <div class="weather">{{ weather.weather[0].main }}</div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </section>
</template>

<script>
export default {
  name: 'Weather',
  components: {},
  data () {
    return {
      api_key: '456d0f88d76e1c3d27b19bc03b54be7a',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weatherList: [],
    }
  },
  methods: {
    getClassWeather(weather) {
      return typeof weather.main != 'undefined' && weather.main.temp > 16
        ? 'night'
        : '';
    },
    fetchWeather (e) {
      if(e.key === "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).then(res => {
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults (results) {
      this.weatherList.push(results);
    },
    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "Match", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`;
    }
  }
};
</script>

<style scoped>
#weather {
  background-image: url('./assets/cold-bg.png');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  min-height: 100vh;
  padding: 25px;
}

#weather.night {
  background-image: url("assets/night-bg.png");
}

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 600;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  margin: 20px 0 0 0;
  color: #fff;
  font-size: 20px;
  font-weight: 400;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 800;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 800;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0 16px 0 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0 16px  0;
}

.weather-list {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}

.weather-wrap {
  margin: 30px 20px;
}
</style>
