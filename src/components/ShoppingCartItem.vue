<template>
  <li class="list-group-item d-flex justify-content-between align-items-center">
    <div class="d-flex align-items-center">
      <img :src="getImageUrl(item.image)" :alt="item.name" class="product-img-sm" />
      <div class="ms-3">
        <div>{{ item.name }}</div>
        <small>Cantidad: {{ item.quantity }}</small>
      </div>
    </div>
    <button class="btn btn-danger btn-sm" @click="$emit('removeFromCart', item.id)">
      <i class="bi bi-trash"></i>
      <span class="d-none d-md-inline ms-1">Eliminar</span>
    </button>
  </li>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  emits: ['removeFromCart'],
  methods: {
    getImageUrl(name) {
      return new URL(`../assets/img/${name}`, import.meta.url).href
    },
  },
}
</script>

<style scoped>
.product-img-sm {
  width: 50px;
  height: 50px;
  object-fit: contain;
}
</style>
