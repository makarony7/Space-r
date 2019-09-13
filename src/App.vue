<template>
  <div :class="[{flexStart: step === 1}, 'wrapper']">
    <transition name="slide">
      <img src="./assets/logo.png" alt="logo" class="logo" v-if="step === 1" />
    </transition>
    <transition name="fade">
      <SpaceBg v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step=== 1" />
    <div class="results" v-if="results && !loading && step ===1">
      <Item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <div class="loader" v-if="step === 1 && loading">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
  </div>
</template>

<script>
import Claim from "@/components/Claim.vue";
import SearchInput from "@/components/SearchInput.vue";
import SpaceBg from "./components/SpaceBg.vue";
import axios from "axios";
import debounce from "lodash.debounce";
import Item from "@/components/Item.vue";
import Modal from "@/components/Modal.vue";

const API = "https://images-api.nasa.gov";

export default {
  name: 'App',
  components: {
    Claim,
    SearchInput,
    SpaceBg,
    Item,
    Modal,
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: "",
      results: [],
      modalOpen: false,
      modalItem: null,
    };
  },
  methods: {
    handleInput: debounce(function() {
      this.loading = true;
      axios
        .get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then(response => {
          this.results = response.data.collection.items;
          console.log(this.searchValue);
          this.loading = false;
          this.step = 1;
        })
        .catch(error => {
          console.log(error);
        });
    }, 500),
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
  },
};
</script>

<style lang="less">
* {
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font-family: "Montserrat", sans-serif;
  margin: 0;
  padding: 0;
}

.wrapper {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  height: 100vh;
  min-height: 100vh;
  color: #fff;
  &.flexStart {
    justify-content: flex-start;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: margin-top 0.3s ease;
}
.slide-enter,
.slide-leave-to {
  margin-top: -50px;
}

.logo {
  position: absolute;
  top: 30px;
  left: 10%;
  max-width: 70px;
}

.results {
  margin-top: 90px;
  color: #000;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 10px;

  @media (min-width: 768px) {
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 30px;
  }
}
.loader {
  margin-top: 50px;
  display: inline-block;
  position: relative;
  width: 100px;
  height: 100px;
}
.loader div {
  animation: loader 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 32px 32px;
}
.loader div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: red;
  margin: -3px 0 0 -3px;
}
.loader div:nth-child(1) {
  animation-delay: -0.036s;
}
.loader div:nth-child(1):after {
  top: 50px;
  left: 50px;
}
.loader div:nth-child(2) {
  animation-delay: -0.072s;
}
.loader div:nth-child(2):after {
  top: 54px;
  left: 45px;
}
.loader div:nth-child(3) {
  animation-delay: -0.108s;
}
.loader div:nth-child(3):after {
  top: 57px;
  left: 39px;
}
.loader div:nth-child(4) {
  animation-delay: -0.144s;
}
.loader div:nth-child(4):after {
  top: 58px;
  left: 32px;
}
.loader div:nth-child(5) {
  animation-delay: -0.18s;
}
.loader div:nth-child(5):after {
  top: 57px;
  left: 25px;
}
.loader div:nth-child(6) {
  animation-delay: -0.216s;
}
.loader div:nth-child(6):after {
  top: 54px;
  left: 19px;
}
.loader div:nth-child(7) {
  animation-delay: -0.252s;
}
.loader div:nth-child(7):after {
  top: 50px;
  left: 14px;
}
.loader div:nth-child(8) {
  animation-delay: -0.288s;
}
.loader div:nth-child(8):after {
  top: 45px;
  left: 10px;
}
@keyframes loader {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>