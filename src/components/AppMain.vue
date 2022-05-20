<template>
  <div class="loader" v-if="loading">
    <AppLoading />
  </div>
  <div class="main" v-else>
    <div class="dropdown-container">
      <AppDropdownGenre @searchGenre="selGenre($event)" :genres="genres" />
      <AppDropdownAuthor @searchAuthor="selAuthor($event)" :authors="authors" />
    </div>
    <div class="cards-container">
      <AppCard
        v-for="(element, index) in filterCards"
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
      genre: "",
      author: "",
      authors: [],
      genres: [],
    };
  },
  created() {
    axios
      .get("https://flynn.boolean.careers/exercises/api/array/music")
      .then((resp) => {
        this.cards = resp.data.response;
        this.success = resp.data.success;
        this.loading = false;
        this.genGenres();
        this.genAuthors();
      });
  },
  computed: {
    filterCards() {
      const newCards = this.cards.filter((element) => {
        return (
          element.genre.includes(this.genre) &&
          element.author.includes(this.author)
        );
      });
      return newCards;
    },
  },
  methods: {
    selGenre(event) {
      this.genre = event;
    },
    genGenres() {
      this.cards.forEach((element) => {
        if (!this.genres.includes(element.genre))
          this.genres.push(element.genre);
      });
    },
    selAuthor(event) {
      this.author = event;
    },
    genAuthors() {
      this.cards.forEach((element) => {
        if (!this.authors.includes(element.author))
          this.authors.push(element.author);
      });
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
  height: calc(100vh - 200px);
  background-color: $main-bg;
  display: flex;
  align-items: center;
  .cards-container {
    width: 45%;
    margin: auto;
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
  margin: auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  align-items: flex-start;
  .box {
    width: 150px;
    color: $text-color;
    background-color: $main-bg;
    border: 2px solid $text-color;
    padding: 0.3rem 5rem 0.3rem 0.5rem;
    margin-bottom: 5%;
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
