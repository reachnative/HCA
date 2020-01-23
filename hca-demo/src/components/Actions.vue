<template>
  <div>
    <Drinks :dispensed="dispensed" :dispense_ready="dispense_ready" :count="count"/>
    <div class="money-inserted">${{ count.toFixed(2) }}</div>
    <button @click="addMoney()" class="insert-money">Insert Money</button>
    <div>
      <button @click="returnMoney()" class="cancel">Cancel</button>
      <button @click="dispenseDrink(); updateStock();" :class="dispenseReady()" :disabled="count < drinkCost">Dispense</button>
    </div>
  </div>
</template>

<script>
import Drinks from './Drinks.vue'
import App from '../App.vue'

export default {
  name: 'Actions',
  components: {
    Drinks
  },
  data: function () {
    return {
      count: 0,
      money: App.data().availableBalance,
      drinkCost: 1.75,
      dispensed: false,
      dispense_ready: false
    }
  },
  methods: {
    addMoney: function () {
      if (this.money > 0 && this.count <= this.drinkCost) {
        if (this.count !== this.drinkCost) {
          this.count += 0.25
          this.money -= 0.25
          this.$emit('balanceCheck', this.money)
          this.dispensed = false
        }
      } else {
        return alert('Oops! Looks like you don\'t have enough money in your wallet!')
      }
    },

    dispenseReady: function () {
      if (this.count === this.drinkCost) {
        this.dispense_ready = true
        return 'dispense'
      } else {
        return 'disabled-dispense'
      }
    },

    returnMoney: function () {
      if (this.count > 0 && this.count <= this.drinkCost) {
        this.money += this.count
        this.count -= this.count
        this.$emit('balanceCheck', this.money)
      }
    },

    dispenseDrink: function () {
      this.count = 0
      this.dispensed = true
      this.dispense_ready = false
    },

    updateStock: function (event) {
      this.$emit('updateStockCount', event)
    }
  }
}
</script>
