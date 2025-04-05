<template>
  <button>hi</button>
</template>

<script lang="ts" setup>
import { ref, defineProps, defineEmits } from 'vue'

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
  coursePlans: Record<string, Record<string, Course>>
  currentPlan: string
}
const props = defineProps<Props>();
const emit = defineEmits(["register-courses", "drop-courses"]);

const selectedCourses = ref<Array<string>>([]);
const conflicts = ref<Array<string>>([]);

const checkForErrors = (planName: string, courseNumbers: string[]) => {
  const seen: Record<string, string[]> = {};
  const conflicts = new Set<string>();

  for (const courseNumber of courseNumbers) {
    const course = props.coursePlans[planName][courseNumber]
    const dateAndTime = course.dates + course.time;

    if (seen[dateAndTime]) {
      conflicts.add(courseNumber);
      seen[dateAndTime].forEach(prev => conflicts.add(prev));
      seen[dateAndTime].push(courseNumber);
    }
    else {
      seen[dateAndTime] = [courseNumber]
    }
  }

  return conflicts.size > 0 ? Array.from(conflicts) : false
}

const dropCourses = (planName: string, courseNumbers: string[], removeFromPlan: boolean) => {
  emit("drop-courses", planName, courseNumbers, removeFromPlan);
}

const registerForClasses = (planName: string, courseNumbers: string[]) => {
  const checkConflicts = checkForErrors(planName, courseNumbers);
  if (checkConflicts === false) {
    emit("register-courses", planName, courseNumbers);
  }
  else {
    conflicts.value = checkConflicts;
  }
}
</script>

<style scoped>

</style>