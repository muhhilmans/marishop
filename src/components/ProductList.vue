<template>
  <div>
    <transition-group
      name="fade"
      tag="div"
      @beforeEnter="before"
      @enter="enter"
      @leave="leave"
    >
      <div
        class="col-lg-6"
        v-for="(item, index) in showItem"
        :key="item.id"
        :data-index="index"
      >
        <div class="card mb-3 shadow">
          <div class="row g-0">
            <div class="col-md-4">
              <img :src="item.image" class="img-fluid rounded-start" />
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h5 class="card-title">{{ item.title }}</h5>
                <p class="card-text">{{ item.description }}</p>
                <div class="d-flex align-items-center justify-content-between">
                  <price :value="Number(item.price)"></price>
                  <button class="btn btn-primary">
                    <font-awesome-icon icon="cart-plus" />
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import Price from "./Price.vue";

export default {
  name: "product-list",
  props: ["products", "maximum"],
  computed: {
    showItem: function () {
      let max = this.maximum;
      return this.products.filter(function (item) {
        return item.price <= max;
      });
    },
  },
  components: {
    FontAwesomeIcon,
    Price,
  },
  methods: {
    before: function (el) {
      el.className = "d-none";
    },
    enter: function (el) {
      var delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeInRight";
      }, delay);
    },
    leave: function (el) {
      var delay = el.dataset.index * 100;
      setTimeout(function () {
        el.className =
          "row d-flex mb-3 align-items-center animated fadeOutRight";
      }, delay);
    },
  },
};
</script>
