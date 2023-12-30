<template>
  <transition-group name="fade" tag="div" @beforeEnter="before" @enter="enter" @leave="leave">
    <div class="row mb-3 align-items-center" v-for="(item, index) in filteredProduct" :key="item.id" :data-index="index">
      <div class="col-1 m-auto">
        <button class="btn btn-info" @click.stop="$emit('add-item', item)">+</button>
      </div>
      <div class="col-sm-4">
        <img class="img-fluid d-block" :src="item.image" :alt="item.name" />
      </div>
      <div class="col">
        <h2 class="text-info">{{ item.name }}</h2>
        <p class="mb-5">{{ item.description }}</p>
        <div class="h5 float-right">
          <price :value="Number(item.price)"></price>
        </div>
      </div>
    </div>
  </transition-group>
</template>

<script>
import Price from "./Price.vue";

export default {
  name: "product-list",
  components: {
    Price
  },
  props: ["products", "maximum"],
  methods: {
    before: function(el) {
      el.className = "d-none";
    },
    enter: function(el) {
      let delay = el.dataset.index * 1000;
      setTimeout(() => {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeInRight";
      }, delay);
    },
    leave: function(el) {
      let delay = el.dataset.index * 100;
      setTimeout(() => {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeOutRight";
      }, delay);
    }
  },
  computed: {
    filteredProduct: function() {
      return this.products.filter(item => item.price <= this.maximum);
    }
  }
};
</script>
