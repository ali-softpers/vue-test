<template>
  <div>
    <Multiselect
      :options="countriesList"
      :searchable="true"
      :filterResults="false"
      :delay="0"
      :multiple="true"
    ></Multiselect>
  </div>
</template>

<script>
import Multiselect from "@vueform/multiselect";
export default {
  components: {
    Multiselect,
  },
  name: "FiltersComponent",
  props: {
    countries: JSON,
    regions: JSON,
  },
  mounted() {
    // alert(window.$(".hello").data("abc"));
  },
  data() {
    return {
      countriesList: this.countries,
      regionsList: this.regions
    };
  },
  created() {
    // this.load();
  },
  methods: {
    // load() {
    //   setTimeout(() => {
    //     // this data comes from an ajax call
    //     this.item = {
    //       id: 1,
    //       // both the commented out value and the
    //       // active value don't work
    //       // relatedItem: {
    //       //   value: 100,
    //       //   label: "test",
    //       // },
    //       relatedItem: 100,
    //     };
    //     this.itemLoaded = true;
    //     console.log(this.item);
    //   }, 250);
    // },
    // async fetchOptions(search) {
    //   console.log(search);
    //   // hits an API
    //   // /api/items/search?search=${search}
    //   return new Promise((resolve) => {
    //     setTimeout(() => {
    //       if (search) {
    //         resolve([
    //           {
    //             this:countries
    //           }
    //         ]);
    //       } else {
    //         resolve([]);
    //       }
    //     }, 200);
    //   });
    // },
  },
};
</script>

<style src="@vueform/multiselect/themes/default.css"></style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
