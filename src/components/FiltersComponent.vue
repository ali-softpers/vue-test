<template>
  <div class="checkbox-select">
    <div class="checkbox-select__trigger" @click="showDropdown">
      <span class="checkbox-select__title">Language</span>
    </div>
    <div class="badge-wrapper">
      <span v-show="displayBadge" class="badge" id="badge">{{
        checkedFilters.length
      }}</span>
    </div>
    <div id="dropdown" class="checkbox-select__dropdown">
      <div class="checkbox-select__search-wrapp">
        <input type="text" placeholder="Search countries" v-model="search" />
      </div>
      <ul
        data-simplebar
        class="customScroll checkbox-select__filters-wrapp"
        data-simplebar-auto-hide="false"
      >
        <li @change="checkBadge" v-for="filter in filteredList" :key="filter">
          <div class="checkbox-select__check-wrapp float-start">
            <input
              :id="filter"
              class="conditions-check"
              v-model="checkedFilters"
              :value="filter"
              type="checkbox"
            />
            <label :for="filter">{{ filter }}</label>
          </div>
        </li>
      </ul>
      <div class="checkbox-select__search-wrapp">
        <input type="text" placeholder="Search regions" v-model="search2" />
      </div>
      <ul class="checkbox-select__filters-wrapp">
        <li
          @change="checkBadge"
          v-for="filter2 in filteredList2"
          :key="filter2"
        >
          <div class="checkbox-select__check-wrapp float-start">
            <input
              :id="filter2"
              class="conditions-check"
              v-model="checkedFilters"
              :value="filter2"
              type="checkbox"
            />
            <label :for="filter2">{{ filter2 }}</label>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { TweenMax, Power2 } from "greensock";

export default {
  name: "FiltersComponent",
  props: {
    countries: JSON,
    regions: JSON,
  },
  // data () {
  //   return {
  //     countriesList : this.countries,
  //     regionsList : this.regions
  //   }
  // },
  data() {
    return {
      filters: this.countries,
      filters2: this.regions,
      search: "",
      search2: "",
      checkedFilters: [],
      activeTrigger: false,
      dropdown: false,
      showLoader: false,
      displayBadge: false,
    };
  },
  computed: {
    filteredList() {
      return this.filters.filter((item) => {
        return item.toLowerCase().includes(this.search.toLowerCase());
      });
    },
    filteredList2() {
      return this.filters2.filter((item) => {
        return item.toLowerCase().includes(this.search2.toLowerCase());
      });
    },
  },
  methods: {
    showDropdown: function () {
      if (this.dropdown == false) {
        this.dropdown = true;
        this.activeTrigger = true;
        TweenMax.fromTo(
          "#dropdown",
          0.55,
          {
            autoAlpha: 0,
            y: -10,
          },
          {
            autoAlpha: 1,
            y: 0,
            ease: Power2.easeOut,
          }
        );
      } else {
        this.dropdown = false;
        this.activeTrigger = false;
        TweenMax.to("#dropdown", 0.2, {
          autoAlpha: 0,
          y: -10,
          ease: Power2.easeOut,
        });
      }
    },
    checkBadge: function () {
      if (this.checkedFilters.length > 0) {
        this.displayBadge = true;
      } else {
        this.displayBadge = false;
      }
    },
  },
};
</script>
<style lang="scss">
* {
  outline: none;
  -webkit-tap-highlight-color: rgba(255, 255, 255, 0);
}

*,
:after,
:before {
  box-sizing: border-box;
}

textarea,
input {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border-radius: 0;
}

ul {
  list-style-type: none;
}
li div label {
  position: relative;
  left: -10px;
}

.badge-wrapper {
  position: relative;
  height: 0;
  width: 0;
}

#badge {
  position: absolute;
  top: -60px;
  left: 125px;
  border-radius: 100%;
  background: lightgreen;
  height: auto;
  font-size: 10px;
  width: 20px;
}

.checkbox-select {
  position: relative;
  max-width: 440px;
  width: 100%;
  @media only screen and (max-width: 600px) {
    margin: 100px auto 0;
  }
  &__trigger {
    border-radius: 50px;
    background: #fff
      url("http://res.cloudinary.com/dnhvfgp9c/image/upload/v1521734636/bcg-pattern.png")
      repeat;
    position: relative;
    z-index: 1;
    // box-shadow: 0 0 10px 8px rgba(0, 0, 0, 0.13);
    height: 50px;
    display: flex;
    align-items: center;
    cursor: pointer;
    padding: 0 25px;
    transition: all 0.4s ease;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    @media only screen and (max-width: 600px) {
      padding: 0 15px;
      height: 70px;
    }
    &.isActive {
      border-radius: 10px 10px 0 0;
      background: #f2f2f2
        url("http://res.cloudinary.com/dnhvfgp9c/image/upload/v1521734636/bcg-pattern.png")
        repeat;
      svg {
        transform: rotate(-180deg);
      }
    }
    &:hover {
      background: #f4f4f4
        url("http://res.cloudinary.com/dnhvfgp9c/image/upload/v1521734636/bcg-pattern.png")
        repeat;
    }
    svg {
      width: 28px;
      stroke: 4px;
      transition: all 0.4s ease;
      @media only screen and (max-width: 600px) {
        width: 22px;
      }
    }
  }
  &__title {
    font-size: 20px;
    flex: 1;
    @media only screen and (max-width: 600px) {
      font-size: 19px;
    }
  }
  &__dropdown {
    min-width: max-content !important;
    opacity: 0;
    visibility: hidden;
    background: #fff
      url("http://res.cloudinary.com/dnhvfgp9c/image/upload/v1521734636/bcg-pattern.png")
      repeat;
    position: absolute;
    left: 0;
    right: 0;
    box-shadow: 0 12px 15px 6px rgba(0, 0, 0, 0.1);
    border-radius: 0 0 8px 8px;
    overflow: hidden;
    padding-bottom: 25px;
    &:after,
    &:before {
      position: absolute;
      content: "";
      top: 0;
      display: block;
      height: 4px;
      z-index: 1;
    }
    &:after {
      opacity: 0;
      background: #000;
      left: -200px;
      width: 200px;
      background-color: #2980b9;
      transition: opacity 0.3s ease;
      animation: load 1.8s linear infinite;
      background: linear-gradient(
        135deg,
        rgba(143, 36, 237, 1) 20%,
        rgba(143, 36, 237, 1) 20%,
        rgba(143, 36, 237, 1) 22%,
        rgba(143, 36, 237, 1) 25%,
        rgba(16, 124, 179, 1) 100%
      );
    }
    &:before {
      width: 100%;
      // background-color: #000;
    }
    &.activeSearch {
      &:after {
        opacity: 1;
      }
    }
    .simplebar-scrollbar {
      width: 3px;
      right: 1px;
    }
  }
  &__search-wrapp {
    padding: 10px 25px 5px;
    @media only screen and (max-width: 600px) {
      padding: 10px 15px 5px;
    }
    input {
      width: 100%;
      height: 40px;
      border-width: 0 0 2px;
      border-style: solid;
      border-color: #000;
      font-size: 16px;
      font-family: "Roboto Slab", serif;
      background: transparent;
    }
    ::-webkit-input-placeholder {
      /* Chrome/Opera/Safari */
      color: #b8b8b8;
      opacity: 1;
    }
    ::-moz-placeholder {
      /* Firefox 19+ */
      color: #b8b8b8;
      opacity: 1;
    }
    :-ms-input-placeholder {
      /* IE 10+ */
      color: #b8b8b8;
      opacity: 1;
    }
    :-moz-placeholder {
      /* Firefox 18- */
      color: #b8b8b8;
      opacity: 1;
    }
  }
  &__col {
    display: flex;
    font-size: 12px;
    padding: 0 25px;
    justify-content: space-between;
    text-transform: uppercase;
    @media only screen and (max-width: 600px) {
      padding: 0 15px;
    }
  }
  &__select-all {
    label {
      cursor: pointer;
    }
    input {
      display: none;
    }
  }
  &__filters-wrapp {
    margin-top: 20px;
    height: 140px;
    overflow-y: hidden;
  }

  &__check-wrapp {
    // position: relative;
    // left: -85px;
    padding: 0 25px;
    margin-bottom: 5px;
    @media only screen and (max-width: 600px) {
      padding: 0 15px;
    }
    input[type="checkbox"] {
      display: none;

      & + label {
        position: relative;
        cursor: pointer;
        font-size: 16px;
        line-height: 22px;
        padding-left: 30px;
        display: inline-block;
        -webkit-touch-callout: none;
        -webkit-user-select: none;
        -khtml-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        transition: padding 0.25s ease;
        &:after {
          border: solid 2px #000;
          content: "";
          width: 22px;
          height: 22px;
          top: 0;
          left: 0;
          position: absolute;
        }
        &:before {
          width: 14px;
          height: 14px;
          content: "";
          position: absolute;
          top: 4px;
          left: 4px;
          background-color: #000;
          opacity: 0;
          will-change: transform;
          transform: scale(0.5);
          transition: all 0.2s ease;
        }
        &:hover {
          padding-left: 32px;
        }
      }
      &:checked {
        & + label {
          &:before {
            opacity: 1;
            transform: scale(1);
          }
        }
      }
    }
  }
}

@keyframes load {
  0% {
    left: -200px;
    width: 20%;
  }
  50% {
    width: 40%;
  }
  70% {
    width: 60%;
  }
  80% {
    left: 50%;
  }
  95% {
    left: 120%;
  }
  100% {
    left: 100%;
  }
}

.link {
  position: absolute;
  left: 0;
  bottom: 0;
  padding: 20px;
  z-index: 9999;
  a {
    display: flex;
    align-items: center;
    text-decoration: none;
    color: #fff;
  }
  .fa {
    font-size: 28px;
    margin-right: 8px;
    color: #fff;
  }
}
</style>
