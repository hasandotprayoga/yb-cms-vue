<template>
  <div id="app">

    <section class="section">
      <div class="container">
        <h1 class="title">Escrow</h1>
        <h2 class="subtitle">
          Data pesanan yang terdeteksi sudah masuk escrow
        </h2>

        <Order/>
        
      </div>
    </section>

  </div>
</template>

<script>
import Order from './components/Order.vue'

export default {
  name: 'App',
  components: {
    Order
  }
}
</script>

<style>
</style>
