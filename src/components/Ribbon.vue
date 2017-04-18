<template>
  <div class="ribbon">
    <div class="title">
      {{ title }}
    </div>
    <div class="subtitle">
      {{ subtitle }}
    </div>
    <div class="slot">
      <slot>
      </slot>
    </div>
  </div>
</template>

<script>
export default {
  props: ['title', 'subtitle']
}
</script>

<style scoped>
  .ribbon {
    width: 100%;
    color: #f5f5f5;
    background-color: #1e88e5;
    padding: 3rem 3rem;
  }
  .title {
    font-size: 2rem;
  }
  .subtitle {
    font-size: 1.5rem;
  }
  .slot {
    padding-top: 1rem;
  }
</style>
