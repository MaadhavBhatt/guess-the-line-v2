<script setup lang="ts">
defineProps<{
  isOpen: boolean;
}>();

const emit = defineEmits<{
  close: [];
}>();
</script>

<template>
  <div v-if="isOpen" class="modal-overlay" @click="emit('close')">
    <div class="modal" @click.stop>
      <button class="close-btn" @click="emit('close')">&times;</button>
      <h2>Help</h2>
      <ul>
        <li><code>f(x)</code> refers to the mystery function you need to guess.</li>
        <li>Use the "New Graph" button in the bottom right corner to refresh the graph.</li>
        <li>
          Visit the
          <a href="https://github.com/MaadhavBhatt/guess-the-line-v2" target="_blank" rel="noopener">GitHub repo</a>
          for feature requests, PRs, and feedback.
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;

  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1000;

  display: flex;
  align-items: center;
  justify-content: center;
}

.modal {
  position: relative;
  background-color: var(--clr-bg);
  border-radius: 0.5rem;

  width: 90%;
  max-width: 50rem;
  padding: 2rem;
}

.close-btn {
  position: absolute;
  inset: 2rem 2rem auto auto;

  font-size: 2rem;
  line-height: 1;

  width: 2.5rem;
  aspect-ratio: 1 / 1;
  cursor: pointer;
}

ul {
  list-style: none;
  font-size: 1.6rem;

  display: flex;
  flex-direction: column;
  gap: 1rem;
}
</style>
