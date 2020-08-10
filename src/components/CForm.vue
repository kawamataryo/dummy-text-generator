<template>
  <div class="mb-1">
    <label class="inline-flex items-center mr-3">
      <input
        v-model="language"
        type="radio"
        name="accountType"
        value="ja"
      />
      <span class="ml-2">Ja</span>
    </label>
    <label class="inline-flex items-center">
      <input
          v-model="language"
          type="radio"
          name="accountType"
          value="en"
      />
      <span class="ml-2">En</span>
    </label>
  </div>
  <div class="grid grid-cols-4 gap-2">
    <div class="col-span-3">
      <input
        id="length"
        v-model.number="length"
        class="col shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker leading-tight focus:outline-none focus:shadow-outline"
        type="number"
        placeholder="text length"
        :class="inputClasses"
      />
    </div>
    <div class="col-span-1">
      <button
        class="bg-blue-500 hover:bg-blue-600 text-white font-semibold py-1 h-full w-full border border-blue-400 rounded shadow text-xs"
        @click="emitSubmit"
      >
        COPY
      </button>
    </div>
  </div>
  <p v-if="!isValid" class="text-red-500 text-xs italic">
    Please enter numerical value.
  </p>
</template>

<script>
import { watch, defineComponent, ref, reactive } from "vue";

export default defineComponent({
  emits: ["submit"],
  setup(_, context) {
    const length = ref(500);
    const language = ref("ja");
    const isValid = ref(true);
    const inputClasses = reactive({
      "border-red-500": !isValid.value,
    });

    const validate = () => {
      isValid.value = !isNaN(Number(length.value));
    };

    watch(length, () => {
      validate();
    });

    const emitSubmit = () => {
      if (isValid.value) {
        context.emit("submit", language.value, length.value);
      }
    };

    return {
      length,
      language,
      inputClasses,
      isValid,
      emitSubmit,
    };
  },
});
</script>

<style scoped></style>
