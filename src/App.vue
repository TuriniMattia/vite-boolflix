<template>
  <appHeader />
  <appMain />
</template>

<script>
import appHeader from '/src/components/appHeader.vue';
import appMain from '/src/components/appMain.vue';

export default {
  components: {
    appHeader,
    appMain,
  }
}
</script>

<style lang="scss">
@use '/style/general';
</style>