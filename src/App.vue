<template>
  <nav>
    <router-link to="/">국내</router-link> |
    <router-link to="/about">해외</router-link>
  </nav>
  <router-view/>
  <Topbutton/>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #5b5b5c;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #5b5b5c;

    &.router-link-exact-active {
      color: #458FFF;
    }
  }
}
</style>
