<script>
export default {
    data (){
        return {
          products: [],
          productName:"",
          productoPrice:0,
          searchByProductName:"",
          product:[],

        }
    },
    methods: {
      async getProducts(){     
    let response = await fetch ('http://localhost:3000/products')
    let productsData = await response.json();
    
    this.products = productsData
    },

    submitproduct(){
        //capturar inputs (con V-model)
        //crear objeto
        let newProduct ={
            "name": this.productName,
            "price": this.productoPrice,

        
        }
        console.log(newProduct)
        //llamada a api post de datos
    },
    async searchByName(){
      let response = await fetch (`http://localhost:3000/products?name=${this.searchByProductName}`);
      let productData = await response.json();
      this.product = productData;
    }
}}
</script>

<template>
  <h1> Products:</h1>
<h3>new product</h3>
  <form action="">
    {{ productName }}
    {{ productoPrice }}
    <br>
    <label for="">nombre</label>
<input type="text" name="productName" id="" v-model="productName">
<label for="">precio</label>
<input type="number" name="" id="" v-model="productoPrice">
<button type="submit" @click="submitproduct">Add new</button>
</form>
<h3>Lista de productos</h3>
<p v-if="products.length === 0">No hay productos</p>
  <div v-else v-for="product in products" v-bind:key="product.id">
  <p > {{ product.name }}</p>
  <p> {{ product.price }}</p>
</div>
  <button @click="getProducts"> get all products</button>

  <form action="">
    <h3>Get by name</h3>
    <label for="">filtro</label>
    <input type="text"  v-model="searchByProductName">
    <button type="button" @click="searchByName">Get by name</button>

  </form>

<p v-for="element in product">{{ element.name }}</p>
</template>

<style>

</style>
