<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
  </div>
</template>

<script>
import Claim from "@/components/Claim.vue";
import SearchInput from "@/components/SearchInput.vue";

export default {
  name: "Search",
  components: {
    Claim,
    SearchInput
  }
};
</script>

<style lang="less" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  height: 100vh;
  color: #000;
  background-image: url('../assets/space.jpg');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>