<template>
  <div class="order-page">
    <AddEditOrder
      :order="order"
      :editMode="editMode"
      :addOrder="addOrder"
      :updateOrder="updateOrder"
      :resetEditMode="resetEditMode"
    />
    <OrdersList
      :orders="orders"
      :editOrder="editOrder"
      :deleteOrder="deleteOrder"
    />
  </div>
</template>

<script>
import OrdersList from './OrdersList.vue'
import AddEditOrder from './AddEditOrder.vue'

export default {
  name: 'OrderPage',

  components: {
    AddEditOrder,
    OrdersList,
  },

  data: () => ({
    order: {},
    dialog: false,
    editMode: false,
    selectedOrderIndex: null,
    orders: []
  }),

  created() {
    let self = this
    self.getOrderFromStorage()
  },

  methods: {
    addOrder(order) {
      let self = this
      self.orders = [...self.orders, order]
      self.saveOrderInStorage()
    },
    editOrder(index) {
      let self = this
      const order = self.orders[index]
      self.selectedOrderIndex = index
      self.order = order
      self.editMode = true
    },
    updateOrder(order) {
      let self = this
      self.orders[self.selectedOrderIndex] = order
      self.editMode = false
      self.saveOrderInStorage()
    },
    deleteOrder(orderId) {
      let self = this
      const orders = self.orders.filter((order) => order.id !== orderId)
      self.orders = orders
      self.saveOrderInStorage()
    },
    resetEditMode() {
      let self = this
      self.editMode = false
    },
    saveOrderInStorage() {
      let self = this
      localStorage.setItem('orders', JSON.stringify(self.orders))
    },
    getOrderFromStorage() {
      let self = this
      self.orders = JSON.parse(localStorage.getItem('orders') || '[]')
    }
  }
}
</script>

<style scoped>
.order-page {
  padding: 1rem;
  width: 700px;
  margin: 0 auto;
  background: whitesmoke;
}
</style>