<template>
  <div class="card">
    <div class="card-title">
      {{ product.name }}
    </div>
    <div class="card-body">
      <i class="icofont-10x icofont-{{ product.icon}}"></i>
      <form>
        <div class="row">
          <div class="cell">
            <label>Type:</label>
          </div>
          <div class="cell">
            <em>{{ product.type }}</em>
          </div>
        </div>
        <div class="row">
          <div class="cell">
            <label>Price:</label>
          </div>
          <div class="cell">${{ product.price.USD }}</div>
        </div>
        <div class="row">
          <div class="cell">
            <label>Quantity:</label>
          </div>
          <div class="cell">
            <input type="number" v-model.number="quantity"/> <!-- add new key 'quantity' into the current 'product' object -->
          </div>
        </div>
      </form>
    </div>
    <div class="card-footer">
      <button
        @click="addToCart(product.name, quantity), resetInputValue()"
        class="btn btn-light"
      >
        Add to cart
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['product', 'index', 'addToCart'],
  // add local variable 'quantity', each Card has it's own variable, as it has only one input box
  data: () => ({
    quantity: 0
  }),
  methods: {
    resetInputValue () {
      this.quantity = 0
    }
  },
  watch: {
    quantity: function resetQ (newQuantity) {
      // console.log(this.quantity)
    }
  }
}
</script>
