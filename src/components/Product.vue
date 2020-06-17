<template>
  <div class="product product_horizontal">
    <span class="product_code">Код: {{ product.code.replace(/^0+/, "") }}</span>
    <div class="product_status_tooltip_container">
      <span class="product_status">Наличие</span>
    </div>
    <div class="product_photo">
      <a href="#" class="url--link product__link">
        <img :src="img" />
      </a>
    </div>
    <div class="product_description">
      <a href="#" class="product__link">{{ product.title }}</a>
    </div>
    <div class="product_tags hidden-sm">
      <p>Могут понадобиться:</p>
      <a href="#" class="url--link">подложка,</a>
      <a href="#" class="url--link">плинтус натуральный,</a>
      <a href="#" class="url--link">рулетка,</a>
      <a href="#" class="url--link">набор для укладки ламината,</a>
      <a href="#" class="url--link">ножовка по ламинату,</a>
      <a href="#" class="url--link">гель для стыков ламината Clic Protect.</a>
    </div>
    <div class="product_units">
      <div class="unit--wrapper">
        <div
          :class="{ 'unit--active': unit }"
          @click="setPrice"
          class="unit--select"
        >
          <p class="ng-binding">За {{ product.unitAlt }}</p>
        </div>
        <div
          v-if="!units"
          :class="{ 'unit--active': !unit }"
          @click="setPriceAlt"
          class="unit--select"
        >
          <p class="ng-binding">За {{ product.unit }}</p>
        </div>
      </div>
    </div>
    <p class="product_price_club_card">
      <span class="product_price_club_card_text">По карте<br />клуба</span>
      <span class="goldPrice">{{ Math.floor(price * 100) / 100 }}</span>
      <span class="rouble__i black__i">
        <svg
          version="1.0"
          id="rouble__b"
          xmlns="http://www.w3.org/2000/svg"
          x="0"
          y="0"
          width="30px"
          height="22px"
          viewBox="0 0 50 50"
          enable-background="new 0 0 50 50"
          xml:space="preserve"
        >
          <use
            xmlns:xlink="http://www.w3.org/1999/xlink"
            xlink:href="#rouble_black"
          ></use>
        </svg>
      </span>
    </p>
    <p class="product_price_default">
      <span class="retailPrice">{{ Math.floor(priceAlt * 100) / 100 }}</span>
      <span class="rouble__i black__i">
        <svg
          version="1.0"
          id="rouble__g"
          xmlns="http://www.w3.org/2000/svg"
          x="0"
          y="0"
          width="30px"
          height="22px"
          viewBox="0 0 50 50"
          enable-background="new 0 0 50 50"
          xml:space="preserve"
        >
          <use
            xmlns:xlink="http://www.w3.org/1999/xlink"
            xlink:href="#rouble_gray"
          ></use>
        </svg>
      </span>
    </p>
    <div class="product_price_points">
      <p class="ng-binding">Можно купить за 231,75 балла</p>
    </div>
    <div class="list--unit-padd"></div>
    <div class="list--unit-desc">
      <div class="unit--info">
        <div class="unit--desc-i"></div>
        <div class="unit--desc-t">
          <p>
            <span class="ng-binding">Продается {{ product.unit }}:</span>
            <span class="unit--infoInn">
              {{ product.unitRatio }} {{ product.unit }} ={{
                product.unitRatioAlt
              }}
              {{ product.unitAlt }}.
            </span>
          </p>
        </div>
      </div>
    </div>
    <div class="product__wrapper">
      <div class="product_count_wrapper">
        <div class="stepper">
          <input
            class="product__count stepper-input"
            type="text"
            v-model="amount"
          />
          <span @click="amount++" class="stepper-arrow up"></span>
          <span @click="removeitem" class="stepper-arrow down"></span>
        </div>
      </div>
      <span
        :data-product-id="product.productId"
        class="btn btn_cart"
        data-url="/cart/"
      >
        <svg class="ic ic_cart">
          <use
            xmlns:xlink="http://www.w3.org/1999/xlink"
            xlink:href="#cart"
          ></use>
        </svg>
        <span class="ng-binding">В корзину</span>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: { product: Object },
  data() {
    return {
      price: "",
      priceAlt: "",
      unit: true,
      img: null,
      amount: 1
    };
  },
  methods: {
    setPrice() {
      this.price = this.product.priceGoldAlt;
      this.priceAlt = this.product.priceRetailAlt;
      this.unit = true;
    },
    setPriceAlt() {
      this.price = this.product.priceGold;
      this.priceAlt = this.product.priceRetail;
      this.unit = false;
    },
    setImgPath(prefix) {
      let imageName = this.product.primaryImageUrl.split(".");
      imageName[imageName.length - 2] =
        imageName[imageName.length - 2] + prefix;
      this.img = imageName.join(".");
    },
    removeitem() {
      if (this.amount > 1) {
        this.amount--;
      }
    }
  },
  computed: {
    units() {
      return this.product.unit === this.product.unitAlt;
    }
  },
  mounted() {
    this.setPrice();
    this.setImgPath("_220x220_1");
  }
};
</script>
