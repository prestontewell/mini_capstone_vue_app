<template>
  <div class ="root">
    Show Page
    <p>{{product.name}}</p>
    <p>{{product.price}}</p>
    <p>{{product.image_url}}</p>
    <p>{{product.description}}</p>
  </div>
</template>

<script>

import axios from "axios";

export default {
  data: function () {
    return {
      product: {
        name: "Super Fork",
        price: "6",
        image_url: "https://i.ibb.co/CBDTPyq/green-fork.jpg",
        description: "That's one mean, green fork."
      }
    };
  },


  created: function() {
    axios.get("api/products/" + this.$route.params.id).then(response => {
      console.log(response.data)
      this.recipe = response.data;
    })
  }
}
</script>



