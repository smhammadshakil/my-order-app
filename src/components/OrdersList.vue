<template>
  <v-container>
    <v-row dense>
      <v-col
        v-for="(order, index) in orders"
        :key="order.id"
        :cols="4"
      >
        <v-card
          max-width="200"
          variant="outlined"
        >
          <v-card-header>
            <div>
              <div class="text-overline mb-1">
                {{ order.name }}
              </div>
              <div class="text-h6 mb-1">
                {{ order.price }}
              </div>
              <div class="text-caption">{{ order.type }}</div>
            </div>
          </v-card-header>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              size="small"
              color="error"
              icon="mdi-trash-can"
              @click="deleteOrder(order.id)"
            ></v-btn>
            <v-btn
              size="small"
              color="warning"
              icon="mdi-pencil"
              @click="editOrder(index)"
            ></v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>

export default {
  name: 'OrdersList',
  props: {
    orders: Array,
    editOrder: Function,
    deleteOrder: Function,
  }
}
</script>

<style scoped>
</style>