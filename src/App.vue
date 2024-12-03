<script setup>
import UHeader from "./components/UpperHedder.vue"
import LFooter from "./components/LowerFooter.vue"
</script>

<template>
  <div>
    <UHeader />
  </div>
  <div id="cccs">

  </div>
  <div id="foot">
    <LFooter />
  </div>
</template>

<style scoped>

#foot {
  /* position: absolute; */
  bottom: 0px;
}

#cccs {
  height: 1000px;
}

</style>
