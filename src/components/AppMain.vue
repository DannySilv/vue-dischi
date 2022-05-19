<template>
  <main>
    <div class="cards-container">
      <AppCard
        v-for="(element, index) in cards"
        :key="index"
        :cardObject="element"
      />
    </div>
  </main>
</template>

<script>
import AppCard from "./AppCard.vue";
import axios from "axios";

export default {
  name: "AppMain",
  components: {
    AppCard,
  },
  data() {
    return {
      cards: [],
      success: false,
    };
  },
  created() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((resp) => {
        this.cards = resp.data.response;
        this.success = resp.data.success;
      });
  },
};
</script>

<style lang="scss" scoped>
$header-card-bg: #2e3a46;
$main-bg: #1e2d3b;

main {
  width: 100%;
  height: calc(100vh - 200px);
  background-color: $main-bg;
  display: flex;
  align-items: center;
  .cards-container {
    width: 60%;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }
}

.active {
  border: 2px solid white;
}
</style>
