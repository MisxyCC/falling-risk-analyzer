<script setup lang="ts">
import NavigationBar from '@/components/layout/NavigationBar.vue';
import Footer from '@/components/layout/Footer-component.vue';
</script>

<template>
  <NavigationBar></NavigationBar>
  <RouterView />
  <Footer></Footer>
</template>
