<template>
  <div class="searchWrapper">
    <input id="search"
      name="search"
      :class=" { dark: dark }"
      :value="value"
      @input="handleChange" />
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
  props: {
    dark: {
      type: Boolean,
      default: false,
    },
    value: {
      type: String,
      required: true,
      //   default: 'Moon';
    },
  },
};
</script>

<style lang="less" scoped>
.searchWrapper {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin-top: 50px;
  input {
    color: #fff;
    text-align: center;
    font-size: 18px;
    font-weight: 300;
    height: 30px;
    border: 0;
    background: none;
    border-bottom: 1px solid #fff;
    transition: box-shadow 0.3s ease-out;
    &:focus,
    &:hover {
      outline: none;
      box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.5);
    }
    @media (min-width: 1024px) {
      font-weight: 400;
    }
  }
  .dark {
    color: #1e3d4a;
    border-bottom-color: #1e3d4a;
    &:focus, &:hover {
      box-shadow: 0 10px 20px -8px rgba(#1e3d4a, 0.5);
    }
  }
}
</style>
