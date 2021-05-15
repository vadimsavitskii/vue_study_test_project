<template>
  <div>
    <b-nav vertical>
      <b-nav-item 
        class="nav-list-item"
        v-for="category in categories" 
        :key="category.alias"
        :to="'/categories/' + category.alias"
        >{{ category.title }}</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'LeftMenu',
  components: {
    
  },

  // "call it constructor"
  mounted() {
    axios
      .get("https://euas.person.ee/categories") // get method
      .then(response => { // server response
        this.categories = response.data; // response data assigned to the categories variable
      });
  }, 
  data: function () {
    return {
      count: 1,
      categories: [] // it is empty
    }
  },
}
</script>

<style>
.nav-list-item a {
  color: black !important;
  border: solid transparent 1px;
}

.nav-list-item a:hover {
  text-decoration: none !important;
  color: black !important;
  text-decoration: underline;
  border-bottom: solid black 1px;
  border-top: solid black 1px;
  border-radius: 6px;
  transition: border-color 0.3s ease-out;
  transition-duration: 0.9s;
}
</style>
