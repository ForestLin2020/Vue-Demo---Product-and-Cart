<template>
  <div class="products">
    <main class="wrapper">
      <h1>Products</h1>

      <div class="card-container">
        <ProductCard
          v-for="(product) in inventory.slice(0,6)"
          :key="product.id"
          class="card"
          :inventory="inventory"
          :addToCart="addToCart"
          :product="product"
        />
      </div>
    </main>
  </div>
</template>

<script>
import ProductCard from '@/components/ProductCard.vue'
export default {
  props: ['inventory', 'addToCart'],
  components: {
    ProductCard
  }
}
</script>
