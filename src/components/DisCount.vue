<script setup>
import { defineProps } from "vue";

const props = defineProps({
  disCountState: Number,
});
</script>

<template>
  <v-card
    variant="tonal"
    class="v-card-title font-weight-black bg-cyan-darken-1 text-deep-orange-lighten-1 rounded-xl"
    >지금 결제하면 {{ props.disCountState }}% 할인!</v-card
  >
</template>

<style scoped></style>
