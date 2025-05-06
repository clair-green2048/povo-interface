<template>
  <div class="home-page">
    <span class="title-button">
      <BaseButton :buttonName="'POVO Course Registration'" :buttonWidth="828" :buttonHeight="146" :disabled="true"></BaseButton>
    </span>
    <span class="header-info">Click one of the page buttons below to get started on registration!</span>
    <span class="home-buttons">
      <BaseButton :buttonName="'My Course Plans'" :buttonWidth="364" :buttonHeight="146" @click="emit('toggle-page', 'CoursePlansPage')"></BaseButton>
      <BaseButton :buttonName="'Course Registration'" :buttonWidth="364" :buttonHeight="146" @click="emit('toggle-page', 'CourseRegistrationPage')"></BaseButton>
    </span>
    <span class="home-buttons">
      <BaseButton :buttonName="'View My Schedule'" :buttonWidth="364" :buttonHeight="146" @click="emit('toggle-page', 'SchedulePage')"></BaseButton>
      <BaseButton :buttonName="'Search for Courses'" :buttonWidth="364" :buttonHeight="146" @click="emit('toggle-page', 'SearchPage')"></BaseButton>
    </span>
  </div>
</template>

<script lang="ts" setup>
import { defineEmits } from 'vue';
import BaseButton from '../global/BaseButton.vue'

const emit = defineEmits(["toggle-page"]);

</script>


<style scoped>
.home-page {
  display: flex;
  flex-direction: column;
  gap: 40px; 
  align-items: center; 
  font-family: 'Montserrat', sans-serif;
}

.title-button {
  display: flex;
  margin-top: 60px;
  gap: 40px 200px; 
  justify-content: center;
}

.header-info {
  color: black;
  font-size: 24px;
  font-weight: 700px;
  gap: 40px 200px;
}

.home-buttons {
  display: flex;
  gap: 80px 200px; 
  justify-content: center;
}

</style>
