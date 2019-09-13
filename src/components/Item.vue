<template>
  <div>
    <div :style="style" class="item"></div>
  </div>
</template>

<script>
export default {
  name: 'Item',
  computed: {
    style() {
      return `backgroundImage: url("${this.photo}")`;
    },
  },
  data() {
    return {
      photo: this.item.links[0].href,
      title: this.item.data[0].title,
    };
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="less" scoped>
.item {
  width: 40vw;
  height: 250px;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 50%;

  @media (min-width: 768px) {
    width: 25vw;
  }
}
</style>