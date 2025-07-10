<template>
  <div class="card h-100 shadow-sm">
    <img :src="getImageUrl(product.image)" class="card-img-top p-3" :alt="product.name" />
    <div class="card-body d-flex flex-column">
      <h5 class="card-title">{{ product.name }}</h5>
      <p class="card-text">Precio: ${{ formatPrice(product.price) }}</p>
      <button class="btn btn-primary mt-auto" @click="$emit('addToCart', product)">
        <i class="bi bi-cart-plus"></i> Agregar al carrito
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  emits: ['addToCart'],
  methods: {
    getImageUrl(name) {
      return new URL(`../assets/img/${name}`, import.meta.url).href
    },
    formatPrice(value) {
      return value.toLocaleString('es-CL')
    },
  },
}
</script>

<style scoped>
.card-img-top {
  height: 180px;
  object-fit: contain;
}
.card {
  transition:
    transform 0.2s,
    box-shadow 0.2s;
}
.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}
</style>
