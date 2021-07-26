<template>
  <div id="app">
    <SearchBox :search="fetchCurrentWeather" :isDisabled="loading" />
    <div class="overview">
        <p>{{ currentWeather.name }}</p>
    </div>
  </div>
</template>

<script>
import SearchBox from "@/components/SearchBox";

export default {
  name: "App",
  components: {
    SearchBox
  },
  data() {
    return {
      currentWeather: {},
      loading: false
    };
  },
  methods: {
    async fetchCurrentWeather(query) {
      try {
        this.loading = true;
        const response = await fetch(
          `https://${process.env.VUE_APP_API_PATH}?q=${query}&units=${process.env.VUE_APP_UNITS_OF_MEASUREMENT || "standard"}&appid=${process.env.VUE_APP_API_KEY}`
        );
        const data = await response.json();
        this.currentWeather = data;
      } catch (e) {
        console.log(e.message);
      } finally {
        this.loading = false;
      }
    }
  },
  mounted() {
    this.currentWeather();
  }
};
</script>
