<template>
  <div>
    <header>
      <div class="wallet">
        <div>Wallet: ${{ money.toFixed(2) }}</div>
      </div>
    </header>
  </div>
</template>

<script>
export default {
  name: 'Wallet',
  props: {
    money: {
      type: Number
    }
  },
  watch: {
    money: function () {
      this.availableBalance.push(this.money)
    }
  }
}
</script>
