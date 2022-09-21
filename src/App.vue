<template>
  <div id="app">
    <router-view />
  </div>
</template>

<style lang="less">
html,
body,
#app {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
  background-color: #ccc;
}
#app {
  overflow: hidden;
  > .scroll-wrap {
    overflow: auto;
    height: 100%;
    width: 100%;
  }
}
</style>
