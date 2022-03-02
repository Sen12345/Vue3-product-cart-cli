<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/product" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <div v-on:click="toggleSideBar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart {{ totalQuantity }} </span>
    </div>
  </header>
  <router-view v-bind:invent="inventory" v-bind:addToCart="addToCart" />
  <SideBar
    v-bind:cart="cart"
    v-bind:remove="removeItem"
    v-bind:invent="inventory"
    v-if="showSideBar"
    v-bind:toggle="toggleSideBar"
  />
</template>

<script>
import SideBar from '@/components/SideBar.vue'
import food from '../food.json'

export default {
  components: {
    SideBar
  },
  data () {
    return {
      showSideBar: false,
      inventory: food,
      cart: {}
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += quantity
    },
    toggleSideBar () {
      this.showSideBar = !this.showSideBar
    },
    removeItem (name) {
      delete this.cart[name]
    },
    getPrice (name) {
      const p = this.inventory.find((product) => {
        return product.name === name
      })
      return p.price.USD.toFixed(2)
    }
    // calculateTotal () {
    //   const total = Object.entries(this.cart).reduce((acc, curr, index) => {
    //     return acc + curr[1] * this.getPrice(curr[0])
    //   }, 0)
    //   return total.toFixed(2)
    // }
  }
}
</script>
