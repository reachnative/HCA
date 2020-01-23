<template>
  <div class="drinks">
    <ul>
      <li v-for="(drink, id) in drinks" :key="id">
        <label>
          <input type="radio" :id="drink.id" :name="drink.name" :value="drink.name" v-model="picked">
          <img  :class="[drink.stockCount === 0 ? 'out-of-stock' : null]" :src="drink.image">
        </label>
        <div v-if="drink.stockCount > 0">{{ drink.stockCount }} Left</div>
        <div v-if="drink.stockCount === 0">Out of Stock</div>
      </li>
    </ul>
    <div v-if="picked !== ''">Selected: {{ picked }} is $1.75</div>
    <div>Dispensed Status: <div v-if="dispense_ready === true">Ready</div><div v-if="dispense_ready === false">Pending</div></div>
    <div v-if="picked === ''"></div>
    <button :class="updateClass()"  @click="updateStock">Confirm</button>
  </div>
</template>

<script>
export default {
  name: 'Drinks',
  props: [
    'dispensed',
    'dispense_ready',
    'count'
  ],
  data () {
    return {
      drinks: [
        { id: 1, name: 'Coca-Cola', image: './static/images/drinks/coke_icon.png', stockCount: 10, cost: 1.75 },
        { id: 2, name: 'Sprite', image: './static/images/drinks/sprite_icon.png', stockCount: 10, cost: 1.75 },
        { id: 3, name: 'Water', image: './static/images/drinks/water_icon.png', stockCount: 10, cost: 1.75 }
      ],
      picked: ''
    }
  },
  methods: {
    updateStock: function (i) {
      for (i = 0; i >= 0; i++) {
        if (this.drinks[i].stockCount > 0 && this.dispense_ready === true) {
          if (this.picked === this.drinks[i].name) {
            this.drinks[i].stockCount--
          }
        }
      }
    },
    updateClass: function () {
      if (this.count === 1.75) {
        return 'dispense'
      } else {
        return 'disabled-dispense'
      }
    }
  }
}
</script>
