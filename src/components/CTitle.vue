<template>
  <div class="flex items-center mb-2">
    <img src="/images/icon.png" alt="icon" class="w-8 mr-2" />
    <h1 class="title font-bold text-lg">{{ title }}</h1>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  setup() {
    return {};
  },
});
</script>

<style scoped></style>
