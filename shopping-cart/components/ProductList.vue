<template>
  <ul>
      <li
        v-for="product in products"
        :key="product.id"
      > {{ product.title }} - {{ currency(product.price) }}
        <br>
        <button
            :disabled="!product.inventory"
            @click="addProductToCart(product)"
        > Add to cart
        </button>
      </li>
  </ul>
</template>

<script>
import { computed } from 'vue'
import { useStore } from 'vuex'
import { currency } from '../currency'

export default {
    setup() {
        const store = useStore()
        const products = computed(() => store.state.product.all)
        const addProductToCart = (product) => store.dispatch('cart/addProductToCart', product)

        store.dispatch('products/getAllProducts')
        return {
            products,
            addProductToCart,
            currency
        }
    }
}
</script>

<style>

</style>