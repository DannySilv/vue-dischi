<template>
  <div class="loader" v-if="loading">
    <AppLoading />
  </div>
  <div class="main" v-else>
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
import AppFilter from "./AppFilter.vue"
import axios from "axios";

export default {
  name: "AppMain",
  components: {
    AppCard,
    AppLoading,
    AppFilter,
  },
  data() {
    return {
      cards: [],
      success: false,
      loading: true,
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
</style>
