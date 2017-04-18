<template>
    <div class="ayat">
        {{ ayats }}
    </div>
</template>

<script>
export default {
  props: ['ayats']
}
</script>

<style scoped>
.ayat {
  width: 100%;
  text-align: right;
  font-family: 'Amiri', serif;
  font-size: 3rem;
  padding: 3rem 2rem;
  line-height: 6rem;
}
</style>
