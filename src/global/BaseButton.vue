<template>
  <button class="button"
    :disabled="props.disabled"
    :style="{
      '--button-width': `${buttonWidth}px`,
      '--button-height': `${buttonHeight}px`
    }">
    <div class="text-content" :class="{ disabled: props.disabled }">
      {{ props.buttonName }}
    </div>
  </button>
</template>

<script lang="ts" setup>
import { defineProps } from 'vue'

interface Props {
    buttonName: string
    buttonWidth: number
    buttonHeight: number
    disabled?: boolean
}
const props = defineProps<Props>();
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100..900&family=Roboto:wght@100..900&display=swap');

.button {
  position: relative;
  height: var(--button-height);
  width: var(--button-width);
  display: flex;
  justify-content: center; 
  align-items: center;    
  text-align: center;
  font-family: 'Montserrat', sans-serif;
  font-weight: 500;
  border-radius: 20px;
  background-color: #00843d;
  border: 1px solid transparent; /* reserve space for the border */
  transition: border-color 0.3s ease, background-color 0.3s ease;
}

.button:hover {
  cursor: pointer;
  border: 1px solid #ffffff;
  background-color: #13753A;
}

.button:disabled {
  cursor: default;
  border: 1px solid transparent;
  background-color: #0C2340;
}

.text-content {
  font-size: 36px;
  font-family: 'Montserrat', sans-serif;
  color: #ffffff;
}

.disabled {
  font-family: 'Montserrat', sans-serif;
  font-size: 48px;
  font-weight: 700;
  color: #c99700;
}

</style>