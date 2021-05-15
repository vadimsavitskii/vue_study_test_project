<template>
  <div>
    <b-card
      :title="product.title"
      :img-src="product.image"
      :img-alt="product.title"
      img-top
      style="max-width: 215px;"
      class="mb-2 product-item"
      @click="clicnOnCard"
    >
      <b-card-text>
        {{ product.description }}
        <p class="price"> Starting from: {{ effectivePrice(cheapestOption()) }} EUR</p>
      </b-card-text>

      <b-button :to="'/products/' + product.id"
      variant="info">See details</b-button>
    </b-card>
  </div>
</template>

<script>

export default {
  name: 'ProductItem',
  components: {
  },
    props: {
    product: Object
  },
  data: function () {
    return {

    }
  },
  methods: {
    effectivePrice: function (option) {
      if(option.priceDiscounted !== undefined) {
        return option.priceDiscounted
      } else if(option.discountPercentage !== undefined) {
        return option.price - (option.price * option.discountPercentage)
      } else {
        return option.price
      }
    },
    cheapestOption: function () {
      let cheapest = this.product.options[0] // assign first to the cheapest option
      for (const option of this.product.options) {
        if(this.effectivePrice(option) < this.effectivePrice(cheapest)) {
          cheapest = option
        }
      }
      return cheapest
    },
    clickOnCard: function () {
      this.$router.push('/products/' + this.product.id)
    }
  }
}
</script>

<style>
.product-item {
  margin-right: 0 !important;
  min-width: 296px;
  cursor: pointer;
}
.price {
  font-weight: bold;
}
</style>
