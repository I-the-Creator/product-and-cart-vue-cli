<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
        <span>
          Cart
          <i class="icofont-cart-alt icofont-1x"></i>
        </span>
        <button @click="toggle" class="cart-close">&times;</button>
      </h1>

      <div class="cart-body">
        <table class="cart-table">
          <thead>
            <tr>
              <th><span class="sr-only">Product Image</span></th>
              <th>Product</th>
              <th>Price</th>
              <th>Qty</th>
              <th>Total</th>
              <th><span class="sr-only">Actions</span></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(quantity, key, i) in cart" :key="i">
              <td><i class="icofont-carrot icofont-3x"></i></td>
              <td>{{ key }}</td>
              <td>${{ getPrice(key) }}</td>
              <td class="center">{{ quantity }}</td>
              <td>${{ (quantity * getPrice(key)).toFixed(2) }}</td>
              <td class="center">
                <button @click="remove(key)" class="btn btn-light cart-remove">
                  &times;
                </button>
              </td>
            </tr>
          </tbody>
        </table>

        <p class="center" v-if="!Object.keys(cart).length"><em>No items in cart</em></p>
        <div class="spread">
          <span><strong>Total:</strong> ${{calculateTotal()}}</span>
          <button class="btn btn-light">Checkout</button>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  /* receiving the props from App.js */
  props: [
    'toggle',
    'cart',
    'inventory',
    'remove'
  ],
  methods: {
    /* helper to get price from inventory by product name - key in 'cart' object:
    iterate through'inventory array - this.inventory' items and find product name which is equal to provided argument
    and return its price
    */
    getPrice (name) {
      const product = this.inventory.find((prod) => {
        return prod.name === name
      })
      return product.price.USD
    },
    calculateTotal () {
      if (Object.keys(this.cart).length === 0) {
        /* object has no properties */
        return 0
      } else {
        /* get array of [key, value] arrays out of 'cart' object, and via 'reduce' we calculation the sum on each iteration
    through this array - each time to sum up 'acc' value with 'currentItem * price'
    currentItem - is an array of [key, value] - [Raddishes, X]
    */
        const total = Object.entries(this.cart).reduce(
          (acc, currentItem, index) => {
            return acc + currentItem[1] * this.getPrice(currentItem[0])
          },
          0
        )
        return total.toFixed(2)
      }
    }
  }
}
</script>
