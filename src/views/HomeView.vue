<template>
  <channeINav></channeINav>
  <!-- <AboutView></AboutView> -->
</template>
<script setup lang='ts'>
import axios from 'axios';
import channeINav from '@/components/channeINav.vue';
import AboutView from '@/components/channeINav.vue';
import { ref } from 'vue';
let active = ref(0);

</script>
<style lang='scss' scoped></style>