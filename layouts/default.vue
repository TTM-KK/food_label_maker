<template>
  <div>
    <div class="container-fluid header__bg">
      <div class="header__title container">
        Food Label
        <span class="header__sub__text">PDF</span> Generator
        <div v-if="isHorizon" class="header__link">
          <span style="font-size: 20px">横型</span>
          <nuxt-link to="/vertical" style="padding-left: 30px"
            >縦型へ切り替え</nuxt-link
          >
        </div>
        <div v-if="isVertical" class="header__link">
          <span style="font-size: 20px">縦型</span>
          <nuxt-link to="/" style="padding-left: 30px"
            >横型へ切り替え</nuxt-link
          >
        </div>
      </div>
    </div>
    <Nuxt />
  </div>
</template>

<script>
export default {
  computed: {
    isVertical() {
      return this.$route.path == "/vertical";
    },
    isHorizon() {
      return this.$route.path == "/";
    },
  },
};
</script>

<style>
html {
  font-family: Roboto, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

.header__bg {
  background-color: #c0c0c0;
}
.header__sub__text {
  color: #fff;
  font-weight: bold;
}

.header__title {
  font-size: 34px;
  padding: 30px 0;
  font-weight: bold;
}
.header__link__home {
  text-decoration: none;
  color: #000;
}
.header__link {
  font-size: 18px;
  padding-top: 10px;
}
</style>
