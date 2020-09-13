<template>
  <div id="input-box">
    <input
      @keyup.enter="getWth"
      v-model="cityName"
      type="text"
      placeholder="write the city name then press enter"
    />
  </div>
</template>


<script>
export default {
  data() {
    return {
      cityName: "",
      apiKey: "30860c0b9720377fd81553d6dc70f540",
      baseUrl: "http://api.openweathermap.org/data/2.5/weather?q=",
    };
  },
  methods: {
    getWth() {
      if (this.cityName === "") {
        alert("please enter a city");
      } else {
        fetch(
          `${this.baseUrl}${this.cityName}&units=metric&appid=${this.apiKey}`
        )
          .then((res) => res.json())
          .then((data) => {
            this.$emit("getWth", data);
          });
      }
    },
  },
};
</script>

<style scoped>
#input-box {
  width: 100%;
  margin-bottom: 1rem;
  display: flex;
}

input {
  padding: 0.5rem 1rem;
  border: 1px solid purple;
  border-radius: 5px;
  outline-color: purple;
  flex: 1;
}
</style>