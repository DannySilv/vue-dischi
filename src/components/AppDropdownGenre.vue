<template>
  <select
    @change="$emit('searchGenre', searchGenre)"
    v-model="searchGenre"
    class="dropdown-content"
    name="filter"
    id="filter"
  >
    <option value="" selected>Tutti i generi</option>
    <option
      v-for="(genre, index) in genres"
      :key="`genre-${index}`"
      :value="genre"
    >
      {{ genre }}
    </option>
  </select>
</template>

<script>
export default {
  name: "AppDropdownGenre",
  props: {
    genres: Array,
  },
  data() {
    return {
      searchGenre: "",
    };
  },
};
</script>

<style lang="scss" scoped>
$main-bg: #1e2d3b;
$text-color: #727873;

.dropdown-content {
  background-color: $main-bg;
  width: 150px;
  font-size: 0.7rem;
  font-family: "Ubuntu", sans-serif;
  font-weight: 500;
  border: 2px solid $text-color;
  border-radius: 2rem;
  color: $text-color;
  padding: 0.3rem 0.5rem;
  margin-bottom: 5%;
  text-decoration: none;
  display: block;
  option {
    background-color: $main-bg;
    font-weight: 500;
  }
}
</style>
