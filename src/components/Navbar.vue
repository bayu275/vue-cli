<template>
  <div>
    <nav class="navbar navbar-light fixed-top">
      <div class="navbar-text ml-auto d-flex mr-2">
        <button class="btn btn-sm btn-outline-success" @click="$emit('toggle-slide')">
          <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
        </button>
        <div class="dropdown ml-2" v-if="cart.length > 0">
          <button class="btn btn-success btn-sm dropdown-toggle" id="dropDownCart" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
            <span class="badge badge-pill badge-success">{{ cartQty }}</span>
            <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
            <price :value="Number(cartTotal)"></price>
            <!-- {{cartTotal | currencyFormat}} -->
          </button>
          <div class="dropdown-menu dropdown-menu-right" aria-labelledby="dropDownCart">
            <div v-for="(item, index) in cart" :key="index">
              <div class="dropdown-item-text text-nowrap text-right">
                <span class="badge badge-pill badge-warning mr-1">
                  {{ item.qty }}
                </span>
                <span class="badge bg-secondary">{{ item.product.qty }}</span>
                {{ item.product.name }}
                <b>{{ (item.product.price * item.qty) | currencyFormat }}</b>
                <a href="#" class="badge badge-danger text-white text-decoration-none text-center ml-1" @click.stop="$emit('delete-item', index)">-</a>
              </div>
            </div>
            <router-link class="btn btn-outline-info text-dark float-right mr-2" to="/checkout">Checkout</router-link>
          </div>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Price from "./Price.vue";

export default {
  name: "navbar",
  props: ["cart", "cartQty", "cartTotal"],
  components: {
    FontAwesomeIcon,
    Price
  },
  filters: {
    currencyFormat: function(value) {
      return `Rp ${Number.parseFloat(value).toFixed(2)}`;
    }
  }
};
</script>
