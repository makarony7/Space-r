<template>
  <div class="outherWrapper">
    <div class="innerWrapper">
      <div class="photo">
        <img :src="photo" alt />
      </div>
      <div class="description">
        <h2 class="title">{{ title }}</h2>
        <p class="description">{{ description }}</p>
      </div>
    </div>
    <div class="close" @click="$emit('closeModal')" />
  </div>
</template>

<script>
export default {
  name: 'Modal',
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description;
  },
};
</script>

<style lang="less" scoped>
.outherWrapper {
  position: fixed;
  top: 0;
  left: 0;
  background: #f6f6f6;
  max-width: 100%;

  @media (min-width: 1024px) {
    max-width: 85%;
    width: 100%;
    top: 50px;
    left: 50%;
    transform: translateX(-50%);
    box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
  }
}
.innerWrapper {
  display: flex;
  height: 100%;
  padding: 50px;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  .photo {
    max-width: 90%;
    height: auto;
    background: black;
  }
  img {
    max-width: 100%;
    height: auto;
    max-height: 400px;
    margin: 0 auto;
    display: block;
  }
  .description {
    color: #333;
  }
}
.close {
  position: absolute;
  top: 0;
  right: 0;
  width: 30px;
  height: 30px;
  padding: 30px;
  cursor: pointer;
  &::before,
  &::after {
    position: absolute;
    top: 30px;
    right: 20px;
    content: "";
    width: 20px;
    height: 2px;
    background: #000;
    display: block;
  }
  &::before {
    transform: rotate(45deg);
  }
  &::after {
    transform: rotate(-45deg);
  }
}
</style>