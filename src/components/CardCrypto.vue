<template>
  <div class="card mb-3 shadow-sm">
    <div class="card-body d-flex align-items-center justify-content-between">
      <div class="d-flex align-items-center gap-3">
        <img :src="image" alt="" width="50" height="50" />
        <div>
          <h5 class="card-title mb-0">{{ coinName || '' }} ({{ symbol || '' }})</h5>
          <small>Rank: {{ rank || '-' }}</small>
        </div>
      </div>
      <div class="text-end">
        <h5 class="mb-0">{{ currentPrice || '-' }}</h5>
        <small :class="echangePorcentage >= 0 ? 'text-success' : 'text-danger'">
          {{ echangePorcentage ? echangePorcentage.toFixed(2) : 0 }}%
        </small>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardCrypto',
  props: ['image', 'coinName', 'symbol', 'rank', 'currentPrice', 'echangePorcentage']
}
</script>
