<template>
  <div class="container my-5">
    <h1 class="mb-4">Criptomoedas</h1>

    <div class="mb-3">
      <select v-model="coinSelect" class="form-select mb-2">
        <option v-for="coin in coinOptions" :key="coin.id" :value="coin.id">
          {{ coin.name }}
        </option>
      </select>

      <select v-model="currencySelect" class="form-select">
        <option v-for="curr in currencyOptions" :key="curr" :value="curr">
          {{ curr.toUpperCase() }}
        </option>
      </select>
    </div>

    <button @click="getCoin" class="btn btn-primary mb-4">Buscar</button>

    <CardCrypto
      v-if="coinData"
      :image="coinData.image"
      :coinName="coinData.name"
      :symbol="coinData.symbol"
      :rank="coinData.market_cap_rank"
      :currentPrice="formatPrice(coinData.current_price)"
      :echangePorcentage="coinData.price_change_percentage_24h"
    />
  </div>
</template>

<script>
import api from '@/services.js'
import CardCrypto from '@/components/CardCrypto.vue'

export default {
  components: { CardCrypto },
  data() {
    return {
      coinData: null,
      coinSelect: 'bitcoin',
      currencySelect: 'usd',
      coinOptions: [
        { id: 'bitcoin', name: 'Bitcoin' },
        { id: 'ethereum', name: 'Ethereum' },
        { id: 'litecoin', name: 'Litecoin' },
        { id: 'dogecoin', name: 'Dogecoin' }
      ],
      currencyOptions: ['usd', 'brl', 'eur']
    }
  },
  methods: {
    async getCoin() {
      const res = await api.get('/coins/markets', {
        params: {
          vs_currency: this.currencySelect,
          ids: this.coinSelect
        }
      })
      this.coinData = res.data[0]
    },
    formatPrice(value) {
      if (!value) return '-'
      return new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: this.currencySelect.toUpperCase()
      }).format(value)
    }
  },
  mounted() {
    this.getCoin()
  }
}
</script>
