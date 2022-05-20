<template>
  <div class="card-container">
    <div class="img-container">
      <img :src="cardObject.poster" alt="" />
    </div>
    <h2>{{ cardObject.title }}</h2>
    <h4>{{ cardObject.author }}</h4>
    <h4>{{ cardObject.year }}</h4>
  </div>
</template>

<script>
export default {
  name: "AppCard",
  props: {
    cardObject: Object,
  },
};
</script>

<style lang="scss" scoped>
$header-card-bg: #2e3a46;
$main-bg: #1e2d3b;
$text-color: #727873;

.card-container {
  width: calc(100% / 5 - 15px);
  background-color: $header-card-bg;
  padding: 1.5%;
  margin: 5px 0;
  margin-left: 15px;
  &:hover {
    transform: scale(1.1, 1.1) translateY(-5px);
    opacity: 0.9;
    transition-duration: 1s;
  }
  h2 {
    color: white;
    font-size: 0.7rem;
    text-transform: uppercase;
    text-align: center;
    margin: 15% 0 15%;
  }
  h4 {
    margin: 0;
    font-size: 0.5rem;
    font-weight: 300;
    text-align: center;
    color: $text-color;
  }
}
</style>
