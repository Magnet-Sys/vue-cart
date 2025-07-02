<template>
  <div class="container-fluid my-4 px-4">
    <div class="row gy-5">
      <div class="col-lg-8">
        <h2 class="mb-4">Productos disponibles</h2>
        <div class="row">
          <div v-for="product in products" :key="product.id" class="col-12 col-md-6 col-lg-4 mb-4">
            <div class="card h-100 shadow-sm">
              <img :src="getImageUrl(product.image)" class="card-img-top p-3" :alt="product.name" />
              <div class="card-body d-flex flex-column">
                <h5 class="card-title">{{ product.name }}</h5>
                <p class="card-text">Precio: ${{ formatPrice(product.price) }}</p>
                <b-button variant="primary" class="mt-auto" @click="addToCart(product)">
                  <i class="bi bi-cart-plus"></i> Agregar al carrito
                </b-button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="col-lg-4">
        <div class="sticky-top" style="top: 20px">
          <h2 class="mb-4">Productos en el carrito</h2>
          <div v-if="cart.length === 0" class="alert alert-info">El carrito está vacío.</div>
          <div v-else>
            <ul class="list-group mb-3">
              <li
                v-for="item in cart"
                :key="item.id"
                class="list-group-item d-flex justify-content-between align-items-center"
              >
                <div class="d-flex align-items-center">
                  <img :src="getImageUrl(item.image)" :alt="item.name" class="product-img-sm" />
                  <div class="ms-3">
                    <div>{{ item.name }}</div>
                    <small>Cantidad: {{ item.quantity }}</small>
                  </div>
                </div>
                <b-button variant="danger" size="sm" @click="removeFromCart(item.id)">
                  <i class="bi bi-trash"></i>
                  <span class="d-none d-md-inline ms-1">Eliminar del carrito</span>
                </b-button>
              </li>
            </ul>
            <h3 class="text-end">Total: ${{ formatPrice(totalPrice) }}</h3>
          </div>
        </div>
      </div>
    </div>

    <footer class="text-center text-muted mt-5 py-3">
      <p>
        <span>&copy; 2025</span>
        <br class="d-md-none" />
        <span class="d-none d-md-inline"> - </span>
        <span>Creado por Dianna Monsalve</span>
      </p>
    </footer>
  </div>
</template>

<script>
import { BButton } from 'bootstrap-vue-next'

export default {
  components: {
    BButton,
  },
  data() {
    return {
      products: [
        { id: 1, name: 'Audífono', price: 30000, stock: 3, image: 'audifono.png' },
        { id: 2, name: 'Mouse', price: 20000, stock: 5, image: 'mouse.png' },
        { id: 3, name: 'Teclado', price: 15000, stock: 10, image: 'teclado.png' },
        { id: 4, name: 'Gabinete', price: 35000, stock: 4, image: 'gabinete.png' },
        { id: 5, name: 'Pantalla', price: 175000, stock: 3, image: 'monitor.png' },
        { id: 6, name: 'Silla', price: 150000, stock: 2, image: 'silla.png' },
      ],
      cart: [],
    }
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => total + item.price * item.quantity, 0)
    },
  },
  methods: {
    getImageUrl(name) {
      return new URL(`./assets/img/${name}`, import.meta.url).href
    },
    addToCart(product) {
      const cartItem = this.cart.find((item) => item.id === product.id)
      if (cartItem) {
        if (cartItem.quantity < product.stock) {
          cartItem.quantity++
        } else {
          alert('No hay más unidades disponibles en stock')
        }
      } else {
        this.cart.push({
          ...product,
          quantity: 1,
        })
      }
    },
    removeFromCart(productId) {
      this.cart = this.cart.filter((item) => item.id !== productId)
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

.product-img-sm {
  width: 50px;
  height: 50px;
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
