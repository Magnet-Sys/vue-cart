<template>
  <div class="sticky-top" style="top: 20px">
    <h2 class="mb-4">Productos en el carrito</h2>
    <div v-if="cart.length === 0" class="alert alert-info">El carrito está vacío.</div>
    <div v-else>
      <ul class="list-group mb-3">
        <ShoppingCartItem
          v-for="item in cart"
          :key="item.id"
          :item="item"
          @remove-from-cart="$emit('removeFromCart', item.id)"
        />
      </ul>
      <h3 class="text-end">Total: ${{ formatPrice(totalPrice) }}</h3>
    </div>
  </div>
</template>

<script>
import ShoppingCartItem from './ShoppingCartItem.vue'

export default {
  components: {
    ShoppingCartItem,
  },
  props: {
    cart: {
      type: Array,
      required: true,
    },
    totalPrice: {
      type: Number,
      required: true,
    },
  },
  emits: ['removeFromCart'],
  methods: {
    formatPrice(value) {
      return value.toLocaleString('es-CL')
    },
  },
}
</script>
