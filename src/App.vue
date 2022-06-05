<template>
  <v-app>
    <v-main>
      <OrderPage/>
    </v-main>
  </v-app>
</template>

<script>
import OrderPage from './components/OrderPage.vue'

export default {
  name: 'App',
  
  components: {
    OrderPage,
  },
}
</script>
