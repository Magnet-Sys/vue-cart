<template>
  <div class="row">
    <div v-for="product in products" :key="product.id" class="col-12 col-md-6 col-lg-4 mb-4">
      <ProductItem :product="product" @add-to-cart="$emit('addToCart', product)" />
    </div>
  </div>
</template>

<script>
import ProductItem from './ProductItem.vue'

export default {
  components: {
    ProductItem,
  },
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
  emits: ['addToCart'],
}
</script>
