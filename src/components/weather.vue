<template>
  <div id="weather">
    <div id="weather_container">
      <Input @getWth="setWth($event)" />
      <div v-if="weather.base !== undefined" id="weather_content">
        <h2 id="city">{{`${weather.name},${weather.sys.country}`}}</h2>
        <p id="time">{{time}}</p>
        <p :class="[{warm:warm},{cold:cold}]" id="temp">{{`${Math.round(weather.main.temp)} C`}}</p>
        <p id="wth">
          {{weather.weather[0].main}}
          <img
            :src="`http://openweathermap.org/img/wn/${weather.weather[0].icon}@2x.png`"
            alt
          />
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import Input from "./input";
export default {
  name: "weather",
  components: { Input },
  data() {
    return { done: false, weather: {}, time: "", warm: false, cold: false };
  },
  methods: {
    checkTemp() {
      if (Math.round(this.weather.main.temp) > 20) {
        this.warm = true;
        this.cold = false;
      } else {
        this.warm = false;
        this.cold = true;
      }
    },
    setWth(wth) {
      this.weather = wth;
      this.checkTemp();
      this.done = true;
      let d = new Date();
      this.time = `${d.getMonth() + 1} / ${d.getDate()}/ ${d.getFullYear()}`;
    },
  },
};
</script>

<style lang="scss" scoped>
#weather {
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 1;
}

#weather_container {
  width: 30%;
}

#weather_content {
  text-align: center;
  & > * {
    margin-bottom: 1rem;
  }
}

.warm {
  color: rgb(255, 115, 0);
}
.cold {
  color: rgb(0, 183, 255);
}

#city,
#wth {
  font-size: 2rem;
  font-weight: bold;
}

#wth {
  display: flex;
  justify-content: center;
  align-items: center;
}

#time {
  font-family: "Work Sans", sans-serif;
  font-size: 1.5rem;
  font-weight: normal;
  color: rgb(97, 97, 97);
}

#temp {
  font-size: 4rem;
  font-weight: bold;
  border: 1px solid purple;
  border-radius: 5px;
  width: max-content;
  margin: auto;
  padding: 2rem;
}
</style>
