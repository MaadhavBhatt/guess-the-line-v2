<script setup lang="ts">
import EmptyModal from './EmptyModal.vue';

defineProps<{
  isOpen: boolean;
}>();

defineEmits<{
  close: [];
}>();
</script>

<template>
  <EmptyModal :isOpen="isOpen" @close="$emit('close')">
    <h2>Help</h2>
    <ul>
      <li>
        <code>f(x)</code> refers to the mystery function you need to guess.
      </li>
      <li>
        Use the "New Graph" button in the bottom right corner to refresh the
        graph.
      </li>
      <li>
        Add new graphs by adding to
        <a
          href="https://github.com/MaadhavBhatt/guess-the-line-v2/edit/main/src/data/graphs.ts"
          target="_blank"
          rel="noopener"
          >this file</a
        >.
      </li>
      <li>
        Visit the
        <a
          href="https://github.com/MaadhavBhatt/guess-the-line-v2"
          target="_blank"
          rel="noopener"
          >GitHub repo</a
        >
        for feature requests and feedback.
      </li>
    </ul>
  </EmptyModal>
</template>

<style scoped>
ul {
  list-style: none;
  font-size: 1.6rem;

  display: flex;
  flex-direction: column;
  gap: 1rem;
}
</style>
