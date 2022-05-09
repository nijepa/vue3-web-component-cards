<template>
  <div class="custom-cards">
    <div
      class="custom-card__wrapper"
      :class="[{ 'h-hide': !active }, { colorized: applyStyle.colorized }]"
    >
      <div class="card stage__card voucher-overview">
        <div class="card-body">
          <h4 class="overview-title text-left">{{ showData.title }}</h4>
          <div id="voucher-history-wrapper" class="d-flex flex-column">
            <div class="loading-spinner hidden"></div>
            <div
              class="custom-card__list"
              v-for="(voucher, i) in testData"
              :key="i"
            >
              <div class="custom-card">
                <div class="custom-card__image">
                  <img
                    :src="`https://images.cadooz.com/${voucher.voucherImage}`"
                    alt="${voucher.name}"
                    class="custom-card__image-container__image"
                  />
                </div>
                <div class="custom-card__details">
                  <div class="">
                    {{ showData.labels[0] }}:
                    <span>{{ voucher.voucherDeliveryDate }}</span>
                  </div>
                  <div class="">
                    {{ showData.labels[1] }}:
                    <span>{{ voucher.voucherValue }}€</span>
                  </div>
                  <div class="">
                    {{ showData.labels[2] }}:
                    <span>{{ voucher.benefitModule }}</span>
                  </div>
                </div>
                <div class="custom-card__list-button ml-sm-auto">
                  <button
                    class="custom-card__button custom-card__button-primary"
                  >
                    {{ showData.button }}
                  </button>
                </div>
              </div>
              <p v-if="showEmptyP" class="product-text text-white">-</p>
            </div>
          </div>
        </div>
        <a
          href="https://employee-benefit-club.n3.cadooztest.com/frontend/view.do;jsessionid=JZMyY2BUB6KRg5ot_lEHizt27xu1kZExYq7_IdYa.betatest03?path=%2Fshop%2Febc%2Forder_history"
          id="to-voucher-history"
          class="custom-card__button custom-card__button-outline custom-card__list-button"
          >Zur Gutscheinhistorie</a
        >
      </div>
    </div>
    <!-- <custom-ca :act="ajaxData" ></custom-ca> -->
  </div>
</template>

<script setup>
import { ref, computed, watch, defineCustomElement } from "vue";
//import CustomCa from './Custom-Ca.ce.vue'

//const CustomCa = defineCustomElement(CardCa);
//customElements.define('custom-ca', CustomCa);
let testData = [
  {
    name: "Test1",
    voucherValue: "10",
    voucherImage:
      "https://images.cadooz.com/addons/product/21/2178/attribute.product.giftcard_image.png",
    voucherRepetitionFrequency: "BMN",
    voucherCurrency: "$",
    voucherDeliveryDate: "25.04.2022",
  },
  {
    name: "IKEA",
    voucherValue: "100",
    voucherImage:
      "https://images.cadooz.com/addons/product/21/2178/attribute.product.giftcard_image.png",
    voucherRepetitionFrequency: "BMN",
    voucherCurrency: "$",
    voucherDeliveryDate: "25.04.2022",
  },
  {
    name: "BestChoice",
    voucherValue: "10000",
    voucherImage:
      "https://images.cadooz.com/addons/product/21/2178/attribute.product.giftcard_image.png",
    voucherRepetitionFrequency: "MON",
    voucherCurrency: "€",
    voucherDeliveryDate: "25.04.3022",
  },
];

const props = defineProps({
  isActive: {
    type: String,
    default: "false",
  },
  cardsData: {
    type: String,
    default: {
      title: "",
      labels: [],
      button: "",
    },
  },
  cardsStyle: {
    type: String,
    default: {
      position: "center",
      decoration: true,
      colorized: false,
      color: "#ffb700",
      font: "'Open Sans', sans-serif",
    },
  },
});

const defaultData = {
  title: "set custom title",
  labels: `<p>* Set component attribute <b>toast-data</b> as JSON object</p>
            <div>
            <p>with following properties: </p>
            <ul>
            <li><i>title</i> <span>(String)</span></li>
            <li><i>message</i> <span>(String - can be used html)</span></li>
            <li><i>type</i> <span>(String - info, success, error)</span></li>
            </ul>
            </div>
            <li>example: </li>
            <p><b><i>const td = { title: 'some title', message: 'message', type: 'info' }</i></b></p>
            <p><b><i>document.querySelector('custom-toast').setAttribute('toast-data', JSON.stringify(td))</i></b></p>
            <br />
            <p>* Styles can be set by setting attribute <b>toast-style</b></p>
            <div>
            <p>with following properties:</p>
            <ul>
            <li><i>position</i> <span>(String - center, left-top, right-top, left-bottom, right-bottom)</span></li>
            <li><i>decoration</i> <span>(Boolean)</span></li>
            <li><i>backdrop</i> <span>(Boolean)</span></li>
            <li><i>colorized</i> <span>(Boolean)</span></li>
            <li><i>color</i> <span>(String - any color)</span></li>
            <li><i>font</i> <span>(String - any font-family)</span></li>
            </ul>
            </div>
            <li>example:</li>
            <p><b><i>const ts = { position: 'center', decoration: false, backdrop: false, color: "#ffffff", font: "'Open Sans', sans-serif" }</i></b></p>
            <p><b><i>document.querySelector('custom-toast').setAttribute('toast-style', JSON.stringify(ts))</i></b></p>`,
};
const showData = computed(() => {
  return props.cardsData ? JSON.parse(props.cardsData) : defaultData;
});
const showEmptyP = computed(() => showData.value.labels.length > 3 || false)
console.log(showData.value);
const defaultStyle = {
  position: "center",
  decoration: false,
  colorized: false,
  backdrop: false,
  color: "#ffb700",
  hoverColor: "#ca981a",
  font: "'Open Sans', sans-serif",
};
const applyStyle = computed(() => {
  return props.cardsStyle ? JSON.parse(props.cardsStyle) : defaultStyle;
});

const ajaxData = ref('55');
const getData = () => {
  fetch("https://jsonplaceholder.typicode.com/todos/")
    .then((response) => response.json())
    .then((data) => console.log(data));
};
getData();

const active = ref(false);
watch(
  () => props.isActive,
  (newValue, oldValue) => {
    // console.log("Watch props.selected function called with args:", newValue, oldValue);
    active.value = newValue === "true";
  }
);

const emit = defineEmits(["close-toast"]);
const toastWrapper = ref(null);
const hideToast = () => {
  active.value = false;
  toastWrapper.value.dispatchEvent(
    new CustomEvent("close-toast", {
      bubbles: true,
      composed: true,
    })
  );
};
</script>
<style>
.custom-cards {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  font-family: v-bind(defaultStyle.font);
}
.stage__card {
  display: flex;
  flex-direction: column;
  height: 100%;
  background-color: transparent;
  border: none;
}

.voucher-overview {
  padding: 1rem;
  background: rgb(255, 255, 255);
  border-radius: 0.5rem;
  box-shadow: 0 0.125rem 0.5rem rgb(0 0 0 / 12%);
}
.custom-card__list {
  display: flex;
  flex-direction: column;
  border-bottom: 1px solid lightgrey;
  padding: 1em 0;
  height: 100%;
}
.custom-card__list-button {
  align-self: flex-end;
  margin-top: 1rem;
}
.custom-card {
  display: flex;
  column-gap: 1em;
  align-items: center;
  font-size: 1rem;
}
.custom-card__image {
  min-width: 120px;
  max-width: 120px;
}
.custom-card__image img {
  width: 100%;
}
.custom-card__image-container__image {
  box-shadow: 0 0.125rem 0.5rem rgb(0 0 0 / 12%);
  border-radius: 0.5rem;
}
img {
  vertical-align: middle;
  border-style: none;
}
.custom-card__list-button {
  align-self: flex-end;
  margin-top: 1rem;
}
.custom-card__button:not(:disabled):not(.disabled) {
  cursor: pointer;
}

[type="button"]:not(:disabled),
[type="reset"]:not(:disabled),
[type="submit"]:not(:disabled),
button:not(:disabled) {
  cursor: pointer;
}

.custom-card__button {
  display: inline-block;
  letter-spacing: -0.0125rem;
  padding: 0.75rem;
  font-weight: 600;
  border-radius: 0.5rem;
  color: #212529;
  text-align: center;
  vertical-align: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  background-color: v-bind(defaultStyle.color);
  border: 1px solid transparent;
  font-size: 1rem;
  line-height: 1.5;
  transition: color 0.15s ease-in-out, background-color 0.15s ease-in-out,
    border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
.custom-card__button:hover {
  background-color: #ca981a;
}
.custom-card__button-primary {
  background-color: v-bind(applyStyle.color);
  color: rgb(255, 255, 255);
  outline: none;
  border: 0;
}
@media (min-width: 576px) {
  .ml-sm-auto,
  .mx-sm-auto {
    margin-left: auto !important;
  }
}
</style>
