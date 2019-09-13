<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">
      Begin Your journey through our amazing galaxy,
      and discover places You never ever heard of!
    </p>
    <p class="subclaim">Type anything space-related to start.</p>
  </div>
</template>

<script>
export default {
  name: "Claim"
};
</script>

<style lang="less" scoped>
.claimWrapper {
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.claim {
  font-size: 50px;
  @media (min-width: 768px) {
    font-size: 80px;
  }
  @media (min-width: 992px) {
    font-size: 100px;
  }
}

.subclaim {
  margin: 20px 0 0 0;
  font-size: 13px;
  font-weight: 400;
  @media (min-width: 768px) {
    width: 500px;
    font-size: 17px;
    letter-spacing: 1px;
  }
}
</style>