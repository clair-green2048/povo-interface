<template>
  <div class="plans-container">
    <span class="plans-sidebar">
      <h2 class="sidebar-title">Plans</h2>
      <BaseButton
        v-for="(courses, planName) in props.coursePlans"
        :key="planName"
        :buttonName="planName"
        :buttonWidth="180"
        :buttonHeight="50"
        @click="emit('select-plan', planName)"
      />
      <BaseButton
        buttonName="New Plan +"
        :buttonWidth="180"
        :buttonHeight="50"
        @click="addNewPlan = !addNewPlan"
      />
      <BaseButton
        buttonName="..."
        :buttonWidth="48"
        :buttonHeight="40"
        class="dots"
      />
    </span>
    <span class="plan-content">
      <div
        class="course-card"
        v-for="(course, courseNumber) in props.coursePlans[currentPlan]"
        :key="courseNumber">
        <div class="course-title">
          {{ courseNumber }} {{ course.name }}
        </div>
        <div class="course-time">
          {{ course.dates }} {{ course.time }}
        </div>
      </div>
    </span>
  </div>
</template>

<script lang="ts" setup>
import { ref, defineProps, defineEmits } from 'vue'
import BaseButton from '../global/BaseButton.vue'

interface Course {
  name: string;
  professor: string;
  time: string;
  dates: string;
  location: string;
  registered?: boolean;
  inPlan? : boolean;
}

interface Props {
  coursePlans: Record<string, Record<string, Course>>;
  currentPlan: string;
}
const props = defineProps<Props>();
const emit = defineEmits(["select-plan", "create-new-plan"])

const addNewPlan = ref<boolean>(false)
// const createNewPlan = (planName: string) => {
//   addNewPlan.value = !addNewPlan.value;
//   emit("create-new-plan", planName)
// }
</script>

<style scoped>
.plans-container {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 40px;
  padding: 40px 0;
  background-color: #002349;
}

.plans-sidebar {
  background-color: #002349;
  width: 220px;
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 12px;
  gap: 12px;
}

.sidebar-title {
  font-weight: bold;
  font-size: 20px;
  color: #fbbf24;
  margin-bottom: 12px;
}

.plan-content {
  width: 400px;
  display: flex;
  flex-direction: column;
  background-color: #002349;
}

.course-card {
  background-color: #00843d;
  color: white;
  padding: 12px 16px;
  margin-bottom: 8px;
  border: 1px solid black;
  font-weight: 600;
  display: flex;
  justify-content: space-between;
}

.course-card.add-class {
  cursor: pointer;
}
</style>