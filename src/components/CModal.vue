<template>
  <div
    class="fixed inset-0 px-2 content-center flex justify-center items-center"
    @click="emitClose"
  >
    <div class="fixed inset-0 transition-opacity">
      <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
    </div>
    <div
      class="bg-white rounded-lg overflow-hidden shadow-xl transform transition-all"
      role="dialog"
      aria-modal="true"
      aria-labelledby="modal-headline"
    >
      <div class="bg-white px-2 pt-2 pb-2">
        <div class="grid grid-cols-5 gap-2 flex items-center">
          <div
            class="mx-auto flex-shrink-0 flex items-center justify-center h-8 w-8 rounded-full bg-green-200 col-span-1"
          >
            <svg
              class="h-4 w-4 text-green-700"
              fill="currentColor"
              viewBox="0 0 20 20"
              stroke="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                clip-rule="evenodd"
              ></path>
            </svg>
          </div>
          <div class="col-span-4">
            <h3 class="font-normal font-bold text-gray-900">
              Copied to clipboard.
            </h3>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  emits: ["close"],
  setup(_, context) {
    const emitClose = () => context.emit("close");
    return { emitClose };
  },
});
</script>

<style scoped></style>
