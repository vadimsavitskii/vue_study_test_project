<template>
  <div>
    <b-navbar toggleable="lg" type="light" variant="dark" class="mb-2">
    <b-navbar-brand to="/" style="color:white; font-family: Consolas; font-size: 19px;">UniElectronics</b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
        <b-nav-item class="b-nav-item" to="/cart">Cart</b-nav-item>
        <b-nav-item class="b-nav-item" to="/orders">Orders</b-nav-item>
        
      </b-navbar-nav>
      
      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <vue-typeahead-bootstrap 
          :data="products"
          :serializer="product => product.title"
          :showOnFocus="true"
          @hit="selectSearchResult"
          @focus="searchFocused"
          inputClass="suggestion-input"
          placeholder="Search for products"
          
        >
        
          <template slot="suggestion" slot-scope="{ data, htmlText }">
            <img class="suggestion-img" :src="data.image"/><span v-html="htmlText"></span>
          </template>
        
        </vue-typeahead-bootstrap>
        
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
  </div>
</template>

<script>
import VueTypeaheadBootstrap from 'vue-typeahead-bootstrap'
import axios from 'axios';

export default {
  name: 'Navigation',
  components: {
    VueTypeaheadBootstrap
  },
    mounted() {
      axios
      .get("https://euas.person.ee/products") // get method
      .then(response => { // server response
        this.products = response.data; // response data assigned to the categories variable
      });
  }, 
  data: function () {
    return {
      products: []
    }
  },
  methods: {
    selectSearchResult: function (product) {
      this.$router.push('/products/' + product.id)
    },
    searchFocused: function () {

    }
  }
}
</script>

<style>
.suggestion-img{
  max-width: 50px;
  margin-right: 10px;
}
input.suggestion-input {
  width: 300px !important;
}

.b-nav-item a {
  color: grey !important;
  border: solid transparent 1px;
  transition-duration: 0.2s;
}

.b-nav-item a:hover {
  text-decoration: none !important;
  color: white !important;
  text-decoration: underline;
  transition-delay: 0.1s;
  transition-timing-function: ease-in-out;
}


</style>
