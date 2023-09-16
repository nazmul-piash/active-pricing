<template>
  <PricingBlock />
  <Footer />
</template>

<script>
import PricingBlock from "./components/PricingBlock.vue";
import Footer from "./components/Footer.vue";

export default {
  components: {
    PricingBlock,Footer
  },
};
</script>

<style>
@import './assets/base.css';
</style>
