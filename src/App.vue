<template>
  <div class="container-fluid my-4 px-4">
    <div class="row gy-5">
      <div class="col-lg-8">
        <h2 class="mb-4">Productos disponibles</h2>
        <ProductList :products="products" @add-to-cart="addToCart" />
      </div>

      <div class="col-lg-4">
        <ShoppingCart :cart="cart" :total-price="totalPrice" @remove-from-cart="removeFromCart" />
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
import ProductList from './components/ProductList.vue'
import ShoppingCart from './components/ShoppingCart.vue'

export default {
  components: {
    ProductList,
    ShoppingCart,
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
  },
}
</script>

<style>
#app {
  display: block;
  padding: 0 2rem;
}
</style>
