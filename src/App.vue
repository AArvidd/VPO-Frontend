<script setup>
import UHeader from "./components/UpperHedder.vue"

import home from "./components/Home.vue"
import searchSite from "./components/SearchSite.vue"

import LFooter from "./components/LowerFooter.vue"

import { ref } from "vue"

let mode = ref(0)


function search(s) {
  mode.value = 1;
}


</script>

<template>
  <div>
    <UHeader @search="search" @home="mode = 0"/>
  </div>
  <div>
    <home v-if="mode == 0"/>
    <searchSite v-else-if="mode == 1" />
  </div>
  <div>
    <LFooter />
  </div>
</template>

<style scoped>

</style>
