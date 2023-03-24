<script setup>
import StopwatchesList from '@/components/StopwatchesList.vue'
</script>

<template>
  <main>
    <StopwatchesList />
  </main>
</template>

<style lang="scss">
main {
  margin: 72px auto 0;
  max-width: 225px;
  @media (min-width: 768px) {
    max-width: 500px;
  }
  @media (min-width: 1024px) {
    max-width: 775px;
  }
}
</style>
