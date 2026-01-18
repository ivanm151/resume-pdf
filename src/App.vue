<script setup>
import Main from './components/Main.vue'
import ExportButton from './components/ExportButton.vue'
</script>

<template>
  <Main id="page" />
  <ExportButton targetId="page" />
</template>

<style>
html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  background: #ccc;
}
</style>
