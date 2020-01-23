<template>
  <div id="app">
    <Wallet :money="availableBalance"/>
    <Actions @balanceCheck="updateBalance" v-model="dispensed"/>
  </div>
</template>

<script>
import Actions from './components/Actions'
import Wallet from './components/Wallet'

export default {
  name: 'App',
  components: {
    Wallet,
    Actions
  },
  data: function () {
    return {
      availableBalance: 50.00,
      dispensed: false,
      inventory: 10
    }
  },
  methods: {
    updateBalance (money) {
      this.availableBalance = money
    }
  }
}
</script>
