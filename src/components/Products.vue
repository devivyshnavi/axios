<template>
  <div>
    <h2>Products</h2>
    <div class="row">
      <div class="col-md-4" v-for="pro in prodata" :key="pro.id">
        <div class="card" style="width: 18rem">
          <img
            class="card-img-top"
            :src="pro.image"
            height="200"
            width="200"
            alt="Card image cap"
          />
          <div class="card-body">
            <h5 class="card-title">{{ pro.pname }}</h5>
            <p class="card-text">{{ pro.quantity }}</p>
            <a
              href="javascript:void(0)"
              class="btn btn-primary"
              v-on:click="addCart(pro.id)"
              >Add to cart</a
            >
            <a
              href="javascript:void(0)"
              class="btn btn-primary"
              v-on:click="delpro(pro.id)"
              >Delete</a
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Products",
  data() {
    return {
      prodata: undefined,
      arr: [],
    };
  },
  methods: {
    delpro(id) {
      console.log(id);
      const URL = "http://localhost:3001/products/";
      if (confirm("Do you want to delete it ?")) {
        axios.delete(`${URL}${id}`).then((res) => {
          if (res) {
            axios.get(URL).then((res) => {
              console.log(res.data);
              this.prodata = res.data;
            });
          }
        });
      }
    },
    addCart(id) {
      const URL = "http://localhost:3001/products/";
      axios.get(`${URL}${id}`).then((res) => {
        alert(id);
        this.arr.push(id);
        localStorage.setItem("items", JSON.stringify(this.arr));
        console.log(res.data);
      });
    },
  },
  mounted() {
    const url = "http://localhost:3001/products";
    axios.get(url).then((res) => {
      console.log(res.data);
      this.prodata = res.data;
    });
  },
};
</script>

<style>
</style>