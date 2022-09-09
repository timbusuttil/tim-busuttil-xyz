<template>
  <BackgroundGradient />
  <router-view/>
</template>

<script>
import BackgroundGradient from '@/components/BackgroundGradient.vue'

export default {
  name: 'App',
  components: {
    BackgroundGradient
  }
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
}
</style>
