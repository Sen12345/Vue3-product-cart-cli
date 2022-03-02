<template>
  <div class="home">
   <div class="splash-container">
        <div class="splash">
          <h1>Splendid Food</h1>
        </div>
      </div>

      <main class="wrapper">

        <h2>Recommended</h2>

        <div class="recommended">

          <Product-card
          v-for="(product, index)
          in invent.slice(0, 3)"
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
// @ is an alias to /src
import ProductCard from '@/components/ProductCard.vue'
export default {
  name: 'HomeView',
  props: ['invent', 'addToCart'],
  components: {
    ProductCard
  }
}
</script>
