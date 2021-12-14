<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <!-- router-link is a substitution of <a> tag-->
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <div @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity }})</span>
    </div>
  </header>

  <router-view :inventory="inventory" :addToCart="addToCart" />

  <Sidebar
    v-if="showSidebar"
    :toggle="toggleSidebar"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"
  />
</template>

<script>
import Sidebar from '@/components/Sidebar.vue'
import food from './food.json'

export default {
  data () {
    return {
      showSidebar: false,
      inventory: food, // array of objects with whole veges
      cart: {} // array of object with name and quantity
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((accumulator, current) => {
        return accumulator + current
      }, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
    },
    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    },
    removeItem (name) {
      delete this.cart[name]
    }
  },
  components: {
    Sidebar
  }
}
</script>
