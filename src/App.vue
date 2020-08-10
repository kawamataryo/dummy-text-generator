<template>
  <div class="container px-3 py-3 mx-auto">
    <CTitle title="Dummy text generator" />
    <CForm @submit="onSubmit" />
    <teleport to="#modal-target">
      <CModal v-if="isDisplayModal" @close="closeModal" />
    </teleport>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import CForm from "./components/CForm.vue";
import { DUMMY_TEXT_EN, DUMMY_TEXT_JA } from "./assets/const";
import CModal from "./components/CModal.vue";
import CTitle from "./components/CTitle.vue";

export default defineComponent({
  name: "App",
  components: {
    CForm,
    CModal,
    CTitle,
  },
  setup: function () {
    const isDisplayModal = ref(false);

    const copyToClipboard = async (text: string) => {
      await navigator.clipboard.writeText(text);
    };

    const onSubmit = async (language: string, length: number) => {
      const dummyText = generateDummyText(language, length);
      await copyToClipboard(dummyText);
      showModal();
    };

    const generateDummyText = (language: string, maxLength: number) => {
      const textSource = language == "en" ? DUMMY_TEXT_EN : DUMMY_TEXT_JA;
      const dummyText = textSource.repeat(
        Math.ceil(maxLength / textSource.length)
      );
      return dummyText.substr(0, maxLength);
    };

    const showModal = () => {
      isDisplayModal.value = true;
    };

    const closeModal = () => {
      isDisplayModal.value = false;
    };

    return {
      onSubmit,
      closeModal,
      isDisplayModal,
    };
  },
});
</script>
