<template>
  <div class="loader" v-if="loading">
    <AppLoading />
  </div>
  <div class="main" v-else>
    <div class="dropdown-container">
      <div class="box dropdown" @click="dropdownToggleGenre()">
        Genere <font-awesome-icon icon="fas fa-chevron-down" class="chevron" />
        <AppDropdownGenre v-show="toggleGenre" />
      </div>
      <div class="box dropdown" @click="dropdownToggleAuthor()">
        Artista <font-awesome-icon icon="fas fa-chevron-down" class="chevron" />
        <AppDropdownAuthor v-show="toggleAuthor" />
      </div>
    </div>
    <div class="cards-container">
      <AppCard
        v-for="(element, index) in cards"
        :key="index"
        :cardObject="element"
      />
    </div>
  </div>
</template>

<script>
import AppCard from "./AppCard.vue";
import AppLoading from "./AppLoading.vue";
import AppDropdownGenre from "./AppDropdownGenre.vue";
import AppDropdownAuthor from "./AppDropdownAuthor.vue";
import axios from "axios";

export default {
  name: "AppMain",
  components: {
    AppCard,
    AppLoading,
    AppDropdownGenre,
    AppDropdownAuthor,
  },
  data() {
    return {
      cards: [],
      success: false,
      loading: true,
      toggleGenre: false,
      toggleAuthor: false,
    };
  },
  created() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((resp) => {
        this.cards = resp.data.response;
        this.success = resp.data.success;
        this.loading = false;
      });
  },
  methods: {
    dropdownToggleGenre() {
      if (this.toggleGenre === false) {
        this.toggleGenre = true;
      } else {
        this.toggleGenre = false;
      }
    },
    dropdownToggleAuthor() {
      if (this.toggleAuthor === false) {
        this.toggleAuthor = true;
      } else {
        this.toggleAuthor = false;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
$header-card-bg: #2e3a46;
$main-bg: #1e2d3b;
$text-color: #727873;

.loader {
  width: 100%;
  height: 100%;
}

.main {
  width: 100%;
  background-color: $main-bg;
  display: flex;
  align-items: center;
  .cards-container {
    width: 60%;
    margin: 3% auto;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }
}

.active {
  border: 2px solid white;
}

.dropdown-container {
  width: 30%;
  margin-left: 5%;
  margin-bottom: 30%;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: flex-start;
  .box {
    width: 40%;
    min-width: 100px;
    color: $text-color;
    background-color: $main-bg;
    border: 2px solid $text-color;
    padding: 0.3rem 5rem 0.3rem 0.5rem;
    font-size: 0.8rem;
    position: relative;
    .chevron {
      position: absolute;
      right: 5%;
      bottom: 25%;
    }
  }
}

.dropdown {
  position: relative;
}
</style>
