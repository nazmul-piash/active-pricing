<template>
  <div class="pricing-card-container">
    <div class="tariff-block">
      <p class="pageviews">{{ pageviewsValue }} </p>
      <div class="price-group">
        <h3 class="price">${{ finalPrice }}.00</h3>
        <span class="period">/ month</span>
      </div>
    </div>

    <input class="pricing-range" v-model="rangeValue" min="1" max="4" type="range" />
    <div class="">
      <div class="period-block">

        <p class="period-paragraph">Yearly Billing </p>
        <label class="period-checkbox-group">
          <input @click="togglePeriod" class="period-checkbox" id="checkbox1" type="checkbox" />
          <span class="period-checkbox-round"></span>
        </label>
        <p class="period-paragraph">
          Overall <span class="discount discount-desc">25% discount</span><span class="discount discount-mob">-25%</span>
        </p>
      </div>
      <div class="period-block">
        <p class="period-paragraph">Life Time Members Billing </p>
        <label class="period-checkbox-group">
          <input @click="togglePeriod" class="period-checkbox" id="checkbox2" type="checkbox" />
          <span class="period-checkbox-round"></span>
        </label>
        <p class="period-paragraph">
          Overall <span class="discount discount-desc">45% discount</span><span class="discount discount-mob">-45%</span>
        </p>
      </div>
    </div>
    <hr class="hr-line" />
  </div>

  <div class="period-block">


  </div>
</template>

<script>
import { ref, watch, onMounted } from "vue";
export default {
  setup() {
    // Variables
    const yearlyBilling = ref(false);
    const lifitimeBilling = ref(false);
    const rangeValue = ref(1);
    const finalPrice = ref(100);
    const rowPrice = ref(100);
    const pageviewsValue = ref();

    onMounted(() => {
      updatePageviews();
    });

    watch(rangeValue, () => {
      updateRowPrice();
      discountCalculation();
      lifetimeDiscountCalculation();
    });

    // Calculate the discount when choosing an yearly billing
    function discountCalculation() {
      if (yearlyBilling.value === true) {
        finalPrice.value = Math.floor(rowPrice.value - rowPrice.value * 0.25);
      } else if (yearlyBilling.value === false) {
        finalPrice.value = rowPrice.value;
      }
      updatePageviews();
    }

    function lifetimeDiscountCalculation() {
      if (lifitimeBilling.value === true) {
        finalPrice.value = Math.floor(rowPrice.value - rowPrice.value * 0.45);
      } else if (lifitimeBilling.value === false) {
        finalPrice.value = rowPrice.value;
      }
      updatePageviews();
    }

    // Choose a payment period

    function togglePeriod() {
      const checkbox1 = document.getElementById("checkbox1");
      const checkbox2 = document.getElementById("checkbox2");

      if (event.target === checkbox1 && event.target !== checkbox2) {

        checkbox2.checked = false;
        yearlyBilling.value = !yearlyBilling.value;
        discountCalculation();
      } else if (event.target === checkbox2 && event.target !== checkbox1) {
        checkbox1.checked = false;
        lifitimeBilling.value = !lifitimeBilling.value;
        lifetimeDiscountCalculation();
      }
    }

    function updateRowPrice() {
      if (rangeValue.value == 1) {
        rowPrice.value = 100;
      } else if (rangeValue.value == 2) {
        rowPrice.value = 300;
      } else if (rangeValue.value == 3) {
        rowPrice.value = 600;
      } else if (rangeValue.value == 4) {
        rowPrice.value = 1200;
      }
    }

    function updatePageviews() {
      if (rangeValue.value == 1) {
        pageviewsValue.value = "1 Month";
      } else if (rangeValue.value == 2) {
        pageviewsValue.value = "3 Monthes";
      } else if (rangeValue.value == 3) {
        pageviewsValue.value = "6 Monthes";
      } else if (rangeValue.value == 4) {
        pageviewsValue.value = "12 Monthes";
      }
    }

    return {
      rangeValue,
      pageviewsValue,
      yearlyBilling,
      lifitimeBilling,
      finalPrice,
      togglePeriod,
    };
  },
};
</script>

<style scoped>
.pricing-card-container {
  width: 600px;
  background-color: var(--c-white);
  border-radius: 10px;
  padding: 50px;
  box-shadow: 5px 5px 30px var(--c-light-grayish-blue),
    -5px -5px 30px var(--c-light-grayish-blue);
}

.tariff-block {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.price-group {
  display: flex;
  align-items: center;
}

.pageviews {
  text-transform: uppercase;
  letter-spacing: 2px;
  font-weight: 800;
}

.price {
  padding-right: 5px;
  font-size: 38px;
  font-weight: 800;
  color: var(--c-dark-desaturated-blue);
}

.pricing-range[type="range"] {
  -webkit-appearance: none;
  width: 100%;
  height: 10px;
  margin: 50px 0;
  padding: 12px 0;
}

.pricing-range[type="range"]::-webkit-slider-thumb {
  pointer-events: none;
  -webkit-appearance: none;
  height: 35px;
  width: 35px;
  border-radius: 50px;
  background-color: var(--c-strong-cyan);
  background-image: url("../assets/images/icon-slider.svg");
  background-position: center center;
  background-repeat: no-repeat;
  cursor: pointer;
  margin-top: -14px;
  transition: 0.3s ease;
}

.pricing-range[type="range"]:hover::-webkit-slider-thumb {
  background-color: var(--c-soft-cyan);
  transition: 0.3s ease;
}

.pricing-range[type="range"]:active::-webkit-slider-thumb {
  background-color: var(--c-strong-cyan);
  transition: 0.3s ease;
}

.pricing-range[type="range"]:focus {
  outline: none;
}

.pricing-range[type="range"]::-ms-track {
  width: 100%;
  cursor: pointer;
  background: transparent;
  border-color: transparent;
  color: transparent;
}

.pricing-range[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  background: var(--c-light-grayish-blue);
  border-radius: 50px;
}

.pricing-range[type="range"]::-ms-fill-lower {
  background-color: #5082e0;
}

.pricing-range[type="range"]::-moz-range-progress {
  background-color: #5082e0;
}

.period-block {
  margin-bottom: 15px;
  display: flex;
  align-items: center;
}

.period-checkbox-group {
  position: relative;
  display: inline-block;
  width: 55px;
  height: 28px;
  margin: 0 20px;
}

.period-checkbox {
  display: none;
}

.period-checkbox:checked+.period-checkbox-round {
  background-color: var(--c-strong-cyan);
}

.period-checkbox:focus+.period-checkbox-round {
  box-shadow: 0 0 1px var(--c-strong-cyan);
}

.period-checkbox:checked+.period-checkbox-round:before {
  transform: translateX(27px);
}

.period-checkbox-round {
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  cursor: pointer;
  background-color: var(--c-light-grayish-blue-toggle);
  transition: 0.4s;
  border-radius: 34px;
  transition: 0.3s ease;
}

.period-checkbox-round:hover {
  background-color: var(--c-soft-cyan);
  transition: 0.3s ease;
}

.period-checkbox-round:before {
  position: absolute;
  content: "";
  width: 20px;
  height: 20px;
  left: 4px;
  bottom: 4px;
  background-color: var(--c-white);
  transition: 0.4s;
  border-radius: 50%;
}

.discount {
  position: absolute;
  margin-left: 10px;
  color: var(--c-light-red);
  background-color: var(--c-light-grayish-red);
  padding: 3px 8px;
  font-size: 13px;
  font-weight: 800;
  border-radius: 50px;
}

.discount-desc {
  display: inline-block;
}

.discount-mob {
  display: none;
}

.hr-line {
  margin: 50px 0 35px 0;
  border: 1px solid var(--c-light-grayish-blue);
  /* border: 2px solid var(--c-very-pale-blue); */
}

.submit-block {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.info-group div {
  display: flex;
  align-items: center;
}

.info-group div img {
  width: 12px;
}

.info-group div p {
  padding: 5px 0 5px 15px;
}

.pricing-btn {
  border: none;
  outline: none;
  background: none;
  cursor: pointer;

  font-family: "Manrope", sans-serif;
  font-size: 15px;
  font-weight: 800;
  background-color: var(--c-dark-desaturated-blue);
  color: var(--c-pale-blue);
  padding: 14px 55px;
  border-radius: 50px;
  transition: 0.3s ease;
}

.pricing-btn:hover {
  color: var(--c-white);
  transition: 0.3s ease;
}

@media screen and (max-width: 768px) {
  .pricing-card-container {
    width: 500px;
  }

  .tariff-block {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .pageviews {
    padding-bottom: 15px;
  }

  .discount-desc {
    display: none;
  }

  .discount-mob {
    display: inline-block;
  }

  .submit-block {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .info-group {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-bottom: 25px;
  }
}

@media screen and (max-width: 580px) {
  .pricing-card-container {
    width: 350px;
  }

  .pricing-range[type="range"] {
    margin: 25px 0;
  }

  .period-block {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .period-checkbox-group {
    margin: 15px 0;
  }
}

@media screen and (max-width: 425px) {
  .pricing-card-container {
    width: 350px;
  }

  .period-block {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .period-checkbox-group {
    margin: 15px 0;
  }
}</style>
