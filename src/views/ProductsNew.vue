<template>
  <div class="home">
    New Product Page
    <div v-for="error in errors">
      {{ error }}
    </div>
    <form v-on:submit.prevent="makeProduct()">
      <p>Name: <input type="text" v-model ="newProductName"></p>
      <p>Description: <input type="text" v-model ="newProductDescription"></p>
      <p>Price: <input type="text" v-model ="newProductPrice"></p>
      <input type="submit" name="Add New Product">
      <!-- <button v-on:click="makeProduct()">Add New Product</button>  -->
    </form>
  </div>
</template>

    



<style>
  img {
    width: 150 px;
  }
</style>

<script>
// @ is an alias to /src
import axios from "axios"

export default {
  data: function() {
    return {
      newProductName: "",
      newProductDescription: "",
      newProductPrice: "",
      errors: []
    };
  },
  created: function() {},

  methods: {
    makeProduct: function() {
      console.log('adding new product');
      var params = {
        name: this.newProductName,
        description: this.newProductDescription,
        price: this.newProductPrice,
        image_url: this.newProductImageUrl
      };

      axios.post("/api/products", params).then(response => {
        console.log('Howm I doin Gary Busey? Great!');
        console.log(response);
        this.$router.push('/');
      }).catch(error => {
        console.log('Terrible Gary Busey!');
        console.log(error)
        console.log(error.response.data.errors);
        this.errors = error.response.data.errors;
      });
    },
    toggleInfo: function(theProduct) {
      if (this.currentProduct === theProduct) {
        this.currentProduct = {};
      }
    },
  }
};
</script>
