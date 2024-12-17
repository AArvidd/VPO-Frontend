<script setup>
import UHeader from "./components/UpperHedder.vue"

import home from "./components/Home.vue"
import searchSite from "./components/SearchSite.vue"
import submition from "./components/Submition.vue"

import LFooter from "./components/LowerFooter.vue"

import { ref, provide } from "vue"

let mode = ref(0);

let searchInput = ref("");

function cahingeView(to) {
  mode.value = to;
}

function sUppdate(s){
  searchInput.value = s;
}

</script>

<template>
  <div id="top">
    <UHeader @chainge="cahingeView" @uppdate="sUppdate"/>
  </div>
  <div id="center">
    <home v-if="mode == 0" @chainge="cahingeView"/>
    <searchSite :search="searchInput" v-else-if="mode == 1" />
    <submition v-else-if="mode == 2" @chainge="cahingeView"/>
  </div>
  <div>
    <LFooter />
  </div>
</template>

<style scoped>

  #top{
    position: sticky;
    top: 0px;
  }

  #center {
    min-height: calc(61vh);
  }
</style>
