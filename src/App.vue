<template>
  <div class="filters">
    <FiltersComponent :countries="countriesJson" :regions="regionsJson" />
    <a
      class="advanced-btn h50"
      id="advanced-btn"
      data-bs-toggle="modal"
      data-bs-target="#exampleModal"
      @click="showModal = true"
    >
      <div class="advanced-btn__title">Advanced Filters</div>
    </a>
    <AdvancedFiltersComponent @clicked="closeModal" v-if="showModal" :all="allJson" />
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
      showModal: false,
    };
  },
  methods: {
    closeModal: function(){
      this.showModal=false;
    }
  },
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
