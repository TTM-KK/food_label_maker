<template>
  <div>
    <div class="container-fluid header__bg">
      <div class="header__title container">
        Food Label
        <span class="header__sub__text">PDF</span> Generator
      </div>
    </div>
    <Nuxt />
  </div>
</template>

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
</style>
