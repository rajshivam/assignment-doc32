<template>
  <div class="home">
    <div class="wrapper">
      <input
        class="city-input"
        v-model="city"
        type="text"
        placeholder="Enter a city name"
      />
      <input
        class="submit-button"
        type="submit"
        value="Get the forecast"
        @click="goToForecast()"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",

  data() {
    return {
      city: null
    };
  },

  methods: {
    //push forecast page in router
    goToForecast() {
      if (this.city)
        this.$router.push({ name: "Forecast", params: { city: this.city } });
      else alert("City name cannot be empty!");
    }
  }
};
</script>

<style lang="scss">
.home {
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.wrapper {
  padding: 4rem 8rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: #7fdbff;
  border-radius: 0.2rem;
}

.city-input {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  padding: 1.5rem 2rem;
  border-radius: 0.2rem;
  background-color: #fff;
  border: none;
  display: block;
  border-bottom: 0.3rem solid transparent;
  transition: all 0.3s;
  &:focus {
    outline: none;
  }
}

.submit-button {
  display: block;
  font-weight: 600;
  color: #000;
  text-transform: uppercase;
  letter-spacing: 1px;
  padding: 1rem 1.5rem;
  overflow: hidden;
  background: #fff;
  border-radius: 0.2rem;
  border: 0;
  cursor: pointer;
  transition: all 0.3s ease;
  &:focus {
    outline-style: none;
  }
}
</style>
