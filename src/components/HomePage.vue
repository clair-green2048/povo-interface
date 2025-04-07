<template>
  <div class="home-page">
    <span class="title-button">
      <BaseButton :buttonName="'POVO Registration Assistant'" :buttonWidth="828" :buttonHeight="146" :disabled="true"></BaseButton>
    </span>
    <span class="home-buttons">
      <BaseButton :buttonName="'Course Plans'" :buttonWidth="364" :buttonHeight="146" @click="emit('toggle-page', 'CoursePlansPage')"></BaseButton>
      <BaseButton :buttonName="'Course Registration'" :buttonWidth="364" :buttonHeight="146" @click="emit('toggle-page', 'CourseRegistrationPage')"></BaseButton>
    </span>
    <span class="home-buttons">
      <BaseButton :buttonName="'View Schedule'" :buttonWidth="364" :buttonHeight="146" @click="emit('toggle-page', 'SchedulePage')"></BaseButton>
      <BaseButton :buttonName="'Search'" :buttonWidth="364" :buttonHeight="146" @click="emit('toggle-page', 'SearchPage')"></BaseButton>
    </span>
  </div>
</template>

<script lang="ts" setup>
import { defineEmits } from 'vue';
import BaseButton from '../global/BaseButton.vue'

const emit = defineEmits(["toggle-page"]);

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.home-page {
  display: flex;
  flex-direction: column;
  gap: 10vh; /* vertical spacing between rows */
  align-items: center; /* optional: center rows horizontally */
}

.title-button {
  display: flex;
  margin-top: 60px;
  gap: 40px 200px; /* horizontal space between buttons */
  justify-content: center;
}

.home-buttons {
  display: flex;
  gap: 40px 200px; /* horizontal space between buttons */
  justify-content: center; /* optional: center buttons in row */
}

</style>
