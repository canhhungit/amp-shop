<template>
  <div class="app">
    <div class="content">
      <nuxt />
    </div>
  </div>
</template>

<script>
export default {
  name: 'DefaultLayout',

  components: {}
}
</script>

<style lang="scss">
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
  color: #ffffff;
  background: #111;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Fira Sans',
    'Droid Sans', 'Helvetica Neue', sans-serif;
  font-size: 15px;
  background-color: #f2f3f5;
  margin: 0;
  padding-top: 55px;
  color: #34495e;
  overflow-y: scroll;
}
a {
  color: #34495e;
  text-decoration: none;
}
.header {
  background-color: #fff;
  position: fixed;
  z-index: 999;
  height: 55px;
  top: 0;
  left: 0;
  right: 0;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  .inner {
    max-width: 960px;
    box-sizing: border-box;
    margin: 0px auto;
    padding: 15px 5px;
  }
  a {
    line-height: 24px;
    transition: color 0.15s ease;
    display: inline-block;
    vertical-align: middle;
    font-weight: 300;
    letter-spacing: 0.075em;
    margin-right: 1.8em;
    margin-right: 1em;
    &:hover {
      color: #808080;
    }
    &.router-link-active {
      color: #fff;
      font-weight: 400;
    }
    &:nth-child(7) {
      margin-right: 0;
    }
  }
  .github {
    font-size: 0.9em;
    margin: 0;
    float: right;
  }
}
.logo {
  width: 24px;
  margin-right: 10px;
  display: inline-block;
  vertical-align: middle;
}
.view {
  max-width: 960px;
  margin: 20px auto 0px auto;
  position: relative;
}
.fade-enter-active,
.fade-leave-active {
  transition: all 0.2s ease;
}
.fade-enter,
.fade-leave-active {
  opacity: 0;
}
.search-header {
  display: inline-block;
  float: right;
}
.search-icon {
  position: absolute;
  top: 20px;
  width: 14px;
  padding: 0 5px;
}
.search-header-input {
  border: 1px solid #808080;
  border-radius: 5px;
  height: 25px;
  padding: 2px 23px 2px 30px;
  background-color: #f5f5f5;
}
input {
  &:focus {
    transition: ease-in-out, width 0.35s ease-in-out;
    width: 250px;
  }
}
@media (max-width: 860px) {
  .header .inner {
    padding: 15px 30px;
  }
}

@media (max-width: 720px) {
  .header {
    .github {
      display: none;
    }
  }
}

@media (max-width: 600px) {
  .header {
    .inner {
      padding: 15px;
    }

    a {
      margin-right: 1em;
    }
  }
}
</style>
