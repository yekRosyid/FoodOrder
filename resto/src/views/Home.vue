<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />
      <div class="row mt-4">
        <div class="col">
          <h3>
            Best
            <strong>Foods</strong>
          </h3>
        </div>
        <div class="col">
          <router-link class="btn btn-success float-right" to="/foods">
            <b-icon-eye></b-icon-eye>Lihat semua
          </router-link>
        </div>
      </div>

      <div class="row">
        <div class="col-md-4 mt-4" v-for="product in products" :key="product.id">
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
import Hero from "../components/Hero.vue";
import CardProduct from "../components/CardProduct";
import axios from "axios";

export default {
  name: "Home",
  components: {
    Navbar,
    Hero,
    CardProduct,
  },

  data() {
    return {
      products: [],
    };
  },

  methods: {
    setProducts(data) {
      this.products = data;
    },
  },

  mounted() {
    axios
      .get("http://localhost:3000/best-products")
      .then((response)=> this.setProducts(response.data))
      .catch((error)=> console.log(error))
  },
};
</script>
