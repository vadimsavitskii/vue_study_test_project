<template>
  <div>
    <h2>Orders</h2>
    <table class="table" v-if="orders && orders.length">
      <thead>
        <tr>
          <th scope="col">Order ID</th>
          <th scope="col">Items</th>
          <th scope="col"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(order, index) in orders" :key="order.id + '-' + index">
          <td># {{ order.id }}</td>
          <td>{{ order.items.length }} item(s)</td>
          <td><b-button variant="info" :to="'/orders/' + order.id">View order</b-button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'OrdersPage',
  components: {

  },
  mounted() {
    axios
      .get("https://euas.person.ee/user/orders") // get method
      .then(response => { // server response
        this.orders = response.data; // response data assigned to the categories variable
    });
  },
  data: function () {
    return {
      orders: []
    }
  }, 
}
</script>

<style>

</style>
