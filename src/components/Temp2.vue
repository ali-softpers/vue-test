<template>
  <button @click="displayButton" class="btn btn-primary rounded-pill" id="location-btn">Location</button>
  <div class="form-control-menu c-scrollbar">
    <div id="d-none" class="form-control-menu-content border" style="display:none">
      <!-- <VueMultiselect
        v-model="selected"
        :options="options">
      </VueMultiselect> -->
      <div class="form-control-menu-group">
        <ul style="overflow: hidden;" v-for="(item) in countriesList" :key="item">
          <li class="d-flex">
            <input type="checkbox" class="">
            <span>{{item}}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
// import VueMultiselect from 'vue-multiselect'
export default {
  // components: { VueMultiselect },
  name: "FiltersComponent",
  props: {
    countries: JSON,
    regions: JSON,
  },
  data () {
    return {
      countriesList : this.countries,
      regionsList : this.regions
    }
  },
  methods: {
    displayButton(){
      document.querySelector("#d-none").style.display="block"
    }
  }
}
</script>

<style src="vue-multiselect/dist/vue-multiselect.css"></style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
/* ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
} */
a {
  color: #42b983;
}
</style>
