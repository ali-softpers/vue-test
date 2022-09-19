<template>
  <!-- Button trigger modal -->

  <!-- Modal -->
  <div
    class="modal fade"
    id="advancedModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
    data-bs-backdrop="static"
    data-bs-keyboard="false"
  >
    <div class="modal-dialog modal-fullscreen">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body p-0 d-flex">
          <div
            class="
              col-2
              text-uppercase
              flex-column
              px-15
              pt-25
              d-flex
              bg-alabaster
              border-right
            "
          >
            <div class="">
              <span
                class="
                  my-15
                  mx-5
                  pt-4
                  px-2
                  float-start
                  pointer
                  color-primary-dark
                  font-weight-bold
                  advanced-filter-tab
                "
                >Overview</span
              >
            </div>
          </div>
          <div class="col-10 p-0 flex-column d-flex justify-content-between">
            <div
              class="
                d-flex
                flex-column
                justify-content-between
                overflow-auto
                h-100
              "
            >
              <div class="c-scrollbar flex-fill p-30 m-10">
                <div class="cusom-scroll float-start p-4 w-100">
                  <div class="title">
                    <span class="f-14 text-uppercase">Location</span>
                  </div>
                  <div class="pt-2 w-25">
                    <input
                      class="form-control"
                      @keyup="checkSuggestion"
                      type="text"
                      placeholder="Search regions"
                      v-model="searchAll"
                      id="searchAll-wrapper-div"
                      :class="{ 'searchAll-wrapper-div-expanded':this.displaySuggestion}"
                    />
                    <div class="form-control-select">
                      <ul
                        v-show="displaySuggestion"
                        class="
                          form-control-menu
                          c-scrollbar
                          mw-100
                          results
                          m-0
                          bg-color-primary
                        "
                        :class="{'searchAll-wrapper-ul-expanded':this.displaySuggestion}"
                        id="searchAll-wrapper-ul"
                      >
                        <li
                          v-for="(filteredValue, index) in filteredJson"
                          :key="index"
                          class="py-1 hovered d-flex align-items-center"
                          @click="addToSelected(filteredValue)"
                        >
                          <span>{{ filteredValue }}</span>
                        </li>
                      </ul>
                    </div>
                  </div>
                </div>
              </div>
              <div class="border-top px-30">
                <ul class="list mb-0 py-15 float-start">
                  <li
                    v-for="(advancedfilter, index) in checkedAdvancedFilters"
                    :key="index"
                    class="list-custom__item mx-3 my-2"
                  >
                    <span class="border px-3 py-2 rounded badge-wrapper">
                      {{ advancedfilter }}
                      <span
                        @click="checkedAdvancedFilters.splice(index, 1)"
                        class="badge bg-color-primary-dark rounded badge-close"
                        >x</span
                      >
                    </span>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="h40 advanced-btn">
            <span class="advanced-btn__title">Apply</span>
          </button>
          <button
            type="button"
            class="btn btn-light rounded-pill text-success"
            data-bs-dismiss="modal"
            @click="this.$emit('clicked')"
          >
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as $ from 'jquery/src/jquery';

export default {
  name: "AdvancedFiltersComponent",
  props: {
    all: JSON,
  },

  data() {
    return {
      allJson: this.all,
      checkedAdvancedFilters: [],
      searchAll: "",
      displaySuggestion: false,
    };
  },
  computed: {
    filteredJson() {
      return this.allJson.filter((item) => {
        return item.toLowerCase().includes(this.searchAll.toLowerCase());
      });
    },
  },
  methods: {
    checkSuggestion: function () {
      if (this.searchAll.length !== 0) {
        this.displaySuggestion = true;
      } else {
        this.displaySuggestion = false;
      }
    },
    addToSelected: function (value) {
      if (!this.checkedAdvancedFilters.includes(value)) {
        this.checkedAdvancedFilters.push(value);
      }
    },
  },
  mounted() {
    $("#advancedModal").modal("show");
  },
};
</script>

<style lang="scss">
.border-right {
  border-right: 1px solid hsla(0, 0%, 44%, 0.12) !important;
}

body {
  font-family: "Roboto Slab", serif;
  padding: 0 15px;
  filter: progid:DXImageTransform.Microsoft.gradient(
      startColorstr="#8f24ed",
      endColorstr="#107cb3",
      GradientType=1
    );
  display: flex;
  align-items: center;
  justify-content: center;
  @media only screen and (max-width: 600px) {
    display: block;
  }
}

.advanced-btn {
  text-decoration: none;
  border: 0;
  background-color: #5abf6e;
  color: #fff !important;
  border-radius: 50px;
  position: relative;
  z-index: 1;
  display: flex;
  align-items: center;
  cursor: pointer;
  padding: 0 25px;
  transition: all 0.4s ease;
  -webkit-user-select: none;
  -moz-user-select: none;
  user-select: none;
  margin-left: 100px;

  &__title {
    white-space: nowrap;
    display: block;
    text-overflow: ellipsis;
    font-size: 20px;
    flex: 1;
  }
}

.color-primary-dark {
  color: #5abf6e !important;
}

.bg-color-primary {
  background-color: #c4ffcf !important;
}

.bg-color-primary-dark {
  background-color: #5abf6e !important;
}

.font-weight-bold {
  font-weight: 600 !important;
}

.h40 {
  height: 40px;
}

.h50 {
  height: 50px;
}

.advanced-btn:hover {
  color: #5abf6e !important;
  background-color: #fff !important;
  border: 1px solid #d3d3d3;
}

.filters {
  display: flex;
}

.custom-scroll {
  overflow: hidden auto;
}

.title {
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  display: -webkit-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-flex-direction: row;
  -ms-flex-direction: row;
  flex-direction: row;
  &::after {
    -webkit-box-flex: 1;
    border-bottom: 1px solid hsla(0, 0%, 44%, 0.12);
    content: "";
    -webkit-flex: 1 1;
    -ms-flex: 1 1;
    flex: 1 1;
    margin: auto auto auto 0.5rem;
  }
}

#searchAll-wrapper-div:focus {
  border-color: #b8b8b8 !important;
  box-shadow: none;
}

#searchAll-wrapper-ul {
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
}

.searchAll-wrapper-div-expanded {
  border-bottom: unset !important;
  border-bottom-left-radius: 0px !important;
  border-bottom-right-radius: 0px !important;
}

.searchAll-wrapper-ul-expanded {
  border-top: unset !important;
  border-top-left-radius: 0px !important;
  border-top-right-radius: 0px !important;
  overflow: hidden;
}

#search {
  border-radius: 1rem;
}

.list-custom {
  list-style: none;
  padding-left: 0;
  &__item {
    display: inline-block;
  }
}
.badge-close {
    position: relative;
    top: -10px;
    left: 40px;
}
</style>