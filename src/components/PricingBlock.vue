<template>
  <div class="pricing-container">
    <div class="wrapper">
      <div class="title-group">
        <h1 class="pricing-title">Traffic-based pricing</h1>
        <h2 class="pricing-subtitle">
         On yearly purchases 25% discount.
        </h2>
      </div>
      <div class="pricing-card">
        <PricingBlockCard />
      </div>
    </div>
  </div>
</template>

<script>
import PricingBlockCard from "./PricingBlockCard.vue";
export default {
  components: {
    PricingBlockCard,
  },
};
</script>

<style scoped>
.pricing-container {
  background-image: url("../assets/images/bg-pattern.svg");
  background-repeat: no-repeat;
  background-size: contain;
  height: 100vh;
}
.title-group {
  padding: 100px 0;
  background-image: url("../assets/images/pattern-circles.svg");
  background-repeat: no-repeat;
  background-position: center center;
  pointer-events: none;
}
.pricing-title,
.pricing-subtitle {
  text-align: center;
  padding: 5px 0;
}
.pricing-title {
  font-weight: 800;
  color: var(--c-dark-desaturated-blue);
}
.pricing-subtitle {
  font-weight: 600;
  font-size: 16px;
}
.pricing-card {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
