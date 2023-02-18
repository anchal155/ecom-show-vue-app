<template>
    <div id="page-wrap">
      <ProductsList :cartItems="cartItems" v-on:remove-from-cart="removeFromCart($event)"/>
    </div>
</template>
<script>
  import axios from 'axios';
  import ProductsList from '@/components/ProductsList.vue';
    export default {
    name: "CartPage",
    data() {
        return {
            cartItems: [],
        };
    },
    methods:{
      async removeFromCart(productId){
        const result = await axios.delete(`/api/users/12345/cart/${productId}`);
        this.cartItems = result.data;
      }
    },
    components: { ProductsList },
    async created(){
      const result = await axios.get('/api/users/12345/cart');
      const cartItems = result.data;
      this.cartItems = cartItems;
    }
}
</script>
