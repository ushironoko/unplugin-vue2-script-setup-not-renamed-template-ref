<script setup lang="ts">
import { ref, computed } from '@vue/composition-api';

const emit = defineEmits<{
  (event: 'input', payload: string): void;
}>();

const handleInput = ({ target }: { target: HTMLInputElement }) => {
  emit('input', target.value);
};

const listeners = computed(() => ({
  input: handleInput,
}))

// renamed to input2 at compile time
const input = ref<HTMLInputElement | null>(null);
const handleClickFocus = () => {  
  input.value?.focus();
};

</script>

<template>
  <div>
    <!-- not renamed ref  -->
    <input ref="input" v-on="listeners" >
    <button @click="handleClickFocus">focus</button>
  </div>
</template>
