<template>
  <div>
    <div class="dropdown-content">
      <a href="#" v-for="(element, index) in cards" :key="index">{{
        element.genre
      }}</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "AppDropdownGenre",
  data() {
    return {
      cards: [],
      success: false,
      loading: true,
      toggle: false,
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
};
</script>

<style lang="scss" scoped>
$header-card-bg: #2e3a46;
$main-bg: #1e2d3b;
$text-color: #727873;

.dropdown-content {
  position: absolute;
  left: -2px;
  top: 23px;
  background-color: $main-bg;
  width: 100px;
  font-size: 0.7rem;
  border: 2px;
  border-top-color: $main-bg !important;
  border-color: $text-color;
  border-style: solid;
  z-index: 1;
}

.dropdown-content a {
  color: $text-color;
  padding: 0.3rem 5rem 0.3rem 0.5rem;
  text-decoration: none;
  display: block;
}

.dropdown-content a:hover {
  background-color: $header-card-bg;
}
</style>
