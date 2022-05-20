<template>
  <select
    @change="$emit('searchAuthor', searchAuthor)"
    v-model="searchAuthor"
    class="dropdown-content"
    name="filter-author"
    id="filter-author"
  >
    <option value="" selected>Tutti gli autori</option>
    <option
      v-for="(author, index) in authors"
      :key="`author-${index}`"
      :value="author"
    >
      {{ author }}
    </option>
  </select>
</template>

<script>
export default {
  name: "AppDropdownAuthor",
  props: {
    authors: Array,
  },
  data() {
    return {
      searchAuthor: "",
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
