<template>
  <div id="app" class="container">
    <router-view
      :cart="cart"
      :cartTotal="cartTotal"
      :cartQty="cartQty"
      :maximum.sync="maximum"
      :products="products"
      :sliderStatus="sliderStatus"
      @toggle="toggleSliderStatus"
      @add="addItem"
      @delete="deleteItem"
    ></router-view>
  </div>
</template>

<script>

export default {
  name: "App",
  data: function() {
    return {
      maximum: 50,
      products: [],
      cart: [],
      sliderStatus: false
    };
  },
  mounted: function() {
    fetch("https://hplussport.com/api/products/order/price")
      .then(res => res.json())
      .then(res => (this.products = res));
  },
  methods: {
    toggleSliderStatus: function() {
      this.sliderStatus = !this.sliderStatus;
    },
    addItem: function(product) {
      let indexProduct;
      let existingProduct = this.cart.find((item, index) => {
        if (item.product.id === product.id) {
          indexProduct = index;
          return true;
        } else {
          return false;
        }
      });
      if (existingProduct) {
        this.cart[indexProduct].qty++;
      } else {
        this.cart.push({ product: product, qty: 1 });
      }
    },
    deleteItem: function(key) {
      if (this.cart[key].qty > 1) {
        this.cart[key].qty--;
      } else {
        this.cart.splice(key, 1);
      }
    }
  },
  computed: {
    cartTotal: function() {
      let sum = 0;
      for (let key in this.cart) {
        sum = sum + this.cart[key].product.price * this.cart[key].qty;
      }
      return sum;
    },
    cartQty: function() {
      let qty = 0;
      for (let key in this.cart) {
        qty = qty + this.cart[key].qty;
      }
      return qty;
    }
  }
};
</script>

<style>
#app {
  margin-top: 4rem;
}
</style>
