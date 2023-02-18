<template>
    <div>
        <ProductsListItem v-for = "product in cartItems" v-on:remove-from-cart="$emit('remove-from-cart', $event)"      :key="product.id" :product="product"/>
        <h3 id="total-price">Total: ${{ totalPrice }}</h3>
        <button id="checkout-button">Proceed to Checkout</button>
    </div>
</template>
<script>
    import ProductsListItem from './ProductsListItem.vue';
    
    export default {
        name:'ProductsList',
        props: ['cartItems'],
        components: {
            ProductsListItem,
        },
        computed: {
          totalPrice(){
            return this.cartItems.reduce(
              (sum, item) => sum + Number(item.price),
              0 
            );
          }
        }
    }
</script>
<style scoped>
      
  #total-price {
    padding: 16px;
    text-align: right;
  }

  #checkout-button {
    width: 100%;
  }
</style>