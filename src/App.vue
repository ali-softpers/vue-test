<template>
  <div class="filters">
    <FiltersComponent :countries="countriesJson" :regions="regionsJson" />
    <AdvancedFiltersComponent :all="allJson" />
  </div>
</template>

<script>
import FiltersComponent from "./components/FiltersComponent.vue";
import AdvancedFiltersComponent from "./components/AdvancedFiltersComponent.vue";
import CountriesJson from "./data/countries.json";
import RegionsJson from "./data/regions.json";

export default {
  name: "App",
  components: {
    FiltersComponent,
    AdvancedFiltersComponent,
  },
  data() {
    return {
      countriesJson: CountriesJson,
      regionsJson: RegionsJson,
      allJson: CountriesJson.concat(RegionsJson),
      
    };
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
