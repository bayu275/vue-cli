<template>
  <transition name="custom-classes-transition" enter-active-class="animated fadeInDown" leave-active-class="animated slideOutRight"
  >
    <div v-if="sliderStatus">
      <div class="align-items-center" :class="sliderState">
        <label class="font-weight-bold mr-2" for="max">Max</label>
        <input type="number" id="max" class="form-control mx-2" v-model="maxAmount" @change="$emit('update:maximum', maxAmount)" style="width: 60px; text-align: center;"
        />
        <input type="range" class="custom-range w-100" min="0" max="200" v-model="maxAmount" @input="$emit('update:maximum', maxAmount)"/>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "price-slider",
  data: function() {
    return {
      maxAmount: 50
    };
  },
  props: ["sliderStatus", "maximum"],
  computed: {
    sliderState: function() {
      return this.sliderStatus ? "d-flex" : "d-none";
    }
  }
};
</script>

<style>
.fade-enter,
.fade-leave {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: all 1s ease-in-out;
}
</style>
