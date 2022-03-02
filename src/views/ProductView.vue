<template>
  <div class="products">
  <main class="wrapper">
        <h1>Products</h1>

        <div class="card-container">
          <Product-card
          v-for="(product, index)
          in invent.slice(0, 6)"
          v-bind:key="index" class="card"
          v-bind:index="index"
          v-bind:product="product"
          v-bind:addToCart="addToCart"
          />
        </div>
      </main>
  </div>
</template>

<script>
import ProductCard from '@/components/ProductCard.vue'

export default {
  props: ['invent', 'addToCart'],
  components: {
    ProductCard
  }
}
</script>
