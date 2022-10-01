<template>
  <div id="app" :style="{ height }">
    <router-view />
  </div>
</template>

<script>
export default {
  data() {
    return {
      height: visualViewport.height + "px",
    };
  },
};
</script>

<style lang="less">
html,
body {
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
  overflow: hidden;
}
#app {
  background: #ccc url("./assets/logo.png") center center no-repeat;
  background-size: 100% 100%;
  overflow: auto;
}
</style>
