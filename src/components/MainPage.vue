<script setup>
import Body from "./custom/body.vue";
defineProps({
  msg: String,
});
</script>

<template>
  <link href="src/style.css" rel="stylesheet" />
  <main class="bg-yellow-50 h-dvh w-screen fixed">
    <Body />
  </main>
</template>
