<script setup lang="ts">
import { onUnmounted } from 'vue'

defineProps<{
  isOpen: boolean
}>()

const emit = defineEmits<{
  close: []
}>()

// Close modal on Escape key press
const handleKeydown = (event: KeyboardEvent) => {
  if (event.key === 'Escape') {
    emit('close')
  }
}
window.addEventListener('keydown', handleKeydown)

// Close modal on clicking outside the modal content / clicking on the overlay
document.querySelector('.modal-overlay')?.addEventListener('click', () => {
  emit('close')
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})
</script>

<template>
  <div v-if="isOpen" class="modal-overlay" @click="emit('close')">
    <div class="modal" @click.stop>
      <button class="close-btn" @click="emit('close')">&times;</button>
      <slot></slot>
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
</style>
