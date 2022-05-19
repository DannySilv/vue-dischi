<template>
  <div id="app">
    <header>
      <AppHeader />
    </header>
    <main>
      <AppMain />
    </main>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";

export default {
  name: "App",
  components: {
    AppHeader,
    AppMain,
  },
};
</script>

<style lang="scss">
@import "./style/style.scss";

#app {
  width: 100%;
  height: calc(100vh - 150px);
  margin: 75px auto;
}
</style>
