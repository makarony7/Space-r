<template>
  <div class="space-img-wrapper"></div>
</template>

<script>
export default {
  name: "SpaceBg"
};
</script>

<style lang="less" scoped>
.space-img-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  z-index: -1;
  width: 100%;
  height: 100vh;
  background-image: url("../assets/space.jpg");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  &:after {
    content: "";
    background: rgba(0, 0, 0, 0.3);
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
    width: 100%;
    height: 100vh;
  }
}
</style>