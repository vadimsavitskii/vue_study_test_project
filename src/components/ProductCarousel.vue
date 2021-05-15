<template>
  <div>
    <b-carousel
      id="carousel"
      :interval="4000"
      controls
      indicators
      background="#ababab"
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
    >

      <router-link :to="'/products/' + product.id" v-for="product in products" :key="product.id">
        <b-carousel-slide 
          :caption="product.title"
          :text="product.description"
          :img-src="product.image"
        ></b-carousel-slide>
      </router-link>


    </b-carousel>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'ProductCarousel',
  components: {
    
  },
  mounted() {
      axios
        .get("https://euas.person.ee/products/") // get method
        .then(response => { // server response
          this.products = response.data; // response data assigned to the categories variable
        });
  }, 
  data: function () {
    return {
      products: []
    }
  }
}
</script>

<style>
#carousel {
  margin-bottom: 20px;
}
</style>
