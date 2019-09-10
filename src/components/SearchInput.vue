<template>
  <div class="searchWrapper">
    <input id="search" name="search" v-model="searchValue" @input="handleInput" />
  </div>
</template>

<script>
import axios from "axios";
import debounce from "lodash.debounce";

const API = "https://images-api.nasa.gov";

export default {
  name: "SearchInput",
  data() {
    return {
      searchValue: "",
      results: []
    };
  },
  methods: {
    handleInput: debounce(function() {
      axios
        .get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then(response => {
          this.results = response.data.collection.items;
        })
        .catch(error => {
          console.log(error);
        });
    }, 500)
  }
};
</script>

<style lang="less" scoped>
.searchWrapper {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin-top: 50px;
  input {
    height: 30px;
    border: 0;
    background: none;
    border-bottom: 1px solid black;
  }
}
</style>