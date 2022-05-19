<template>
  <header>
    <div class="header-container">
      <div class="logo-container">
        <img src="../assets/img/spotify-logo.png" alt="SpotifyLogo" />
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
};
</script>

<style lang="scss" scoped>
$header-card-bg: #2e3a46;
$main-bg: #1e2d3b;

header {
  width: 100%;
  height: 50px;
  background-color: $header-card-bg;
  .header-container {
    width: 90%;
    margin: 0 auto;
    .logo-container {
      display: flex;
      align-items: center;
      height: 50px;
      width: 40px;
    }
  }
}
</style>
