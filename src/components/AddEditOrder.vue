<template>
  <div class="add-order">
    <v-row justify="center">
      <v-dialog
        persistent
        v-model="dialog"
      >
        <template v-slot:activator="{ props }">
          <h2>Orders</h2>
          <v-btn
            size="small"
            variant="text"
            v-bind="props"
            color="success"
            icon="mdi-plus-thick"
          />
        </template>
        <v-card class="wd-500">
          <v-card-title>
            <span class="text-h5">Add Order</span>
          </v-card-title>
          <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field
                  label="Name"
                  v-model="name"
                />
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="Price $"
                  v-model="price"
                  @keypress="onlyNumber"
                />
              </v-col>
              <v-col cols="12">
                <v-autocomplete
                  :items="dataTypes"
                  v-model="type"
                  label="Type"
                />
              </v-col>
            </v-row>
          </v-container>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              @click="close()"
              color="blue-darken-1"
            >
              Cancel
            </v-btn>
            <v-btn
              color="blue-darken-1"
              :disabled="!(name && price && type)"
              @click="editMode ? update() : add()"
            >
              {{ editMode ? 'Update' : 'Add' }}
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-row>
  </div>
</template>

<script>

export default {
  name: 'AddEditOrder',

  props: {
    order: Object,
    editMode: Boolean,
    addOrder: Function,
    updateOrder: Function,
    resetEditMode: Function,
  },

  data: () => ({
    name: '',
    price: '',
    type: '',
    dialog: false,
    dataTypes: [
      'Device Location',
      'Device Behavior',
      'ID Mapping'
    ],
  }),

  methods: {
    add() {
      let self = this
      self.addOrder({
        id: Math.random(),
        name: self.name,
        price: self.price,
        type: self.type,
      })
      self.close()
      self.name = ''
      self.price = ''
      self.type = ''
    },
    update() {
      let self = this
      self.updateOrder({
        id: self.order.id,
        name: self.name,
        price: self.price,
        type: self.type,
      })
      self.close()
      self.name = ''
      self.price = ''
      self.type = ''
    },
    close() {
      let self = this
      self.dialog = false
      self.resetEditMode()
    },
    onlyNumber (e) {
      let keyCode = (e.keyCode ? e.keyCode : e.which);
      if ((keyCode < 48 || keyCode > 57) && keyCode !== 46) { // 46 is dot
          e.preventDefault();
      }
    }
  },

  watch: {
    editMode(newValue) {
      let self = this
      if (newValue) {
        self.name = self.order.name
        self.price = self.order.price
        self.type = self.order.type
        self.dialog = true
      } else {
        self.name = ''
        self.price = ''
        self.type = ''
        self.dialog = false
      }
    }
  }
}
</script>

<style scoped>
.wd-500 {
  min-width: 500px;
}
</style>