<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- <h1>Products: {{ products }}</h1> -->
    <div v-for="product in products">
      <p>{{product.name}}</p>
      <p>{{product.price}}</p>
      <img v-bind:src="product.image_url">
      <button v-on:click="currentProduct = product">Show more info</button>
      <div v-if="product === currentProduct">
        <p>{{product.description}}</p>
        <p>Name: <input type="text" v-model="product.name"></p>
        <p>Price: <input type="text" v-model="product.price"></p>
        <p>Description: <input type="text" v-model="product.description"></p>
        <button v-on:click="updateProduct(product)">Update Product</button>
        <button v-on:click="deletProduct(product)">Delete Product</button>
      </div>
      </div>
    </div>

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
      message: "Welcome to The Store!",
      products: [],
      newProductName: "",
      newProductDescription: "",
      newProductPrice: "",
      currentProduct: {}
    };
  },
  created: function() {
    axios.get("/api/products").then(response => {
      this.products = response.data;
    })
  },

methods: {
  makeProduct: function() {
    var params = {
      name: this.newProductName,
      description: this.newProductDescription,
      price: this.newProductPrice,
      image_url: this.newProductImageUrl
    }

    axios.post("/api/products", params).then(response => {
      console.log(response);
      this.products.push(response.data);
    });
  },
  toggleInfo: function(theProduct) {
    if (this.currentProduct === theProduct) {
      this.currentProduct = {};
    }
  },
  updateProduct: function(theProduct) {
    console.log(theProduct)
    var params = {
      name: theProduct.name,
      description: theProduct.description,
      price: theProduct.price,
      image_url: theProduct.image_url
    };
  }
}

};
</script>
