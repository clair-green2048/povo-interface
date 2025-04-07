<template>
  <div class="search-container">
    <h2 class="search-title">What are you searching for?</h2>
    <textarea class="search-box" placeholder="Find me classes on Tuesday and Thursday for a Math major..."></textarea>
  </div>
  <div v-if="searchEntered"></div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

// interface Course {
//   name: string;
//   professor: string;
//   time: string;
//   dates: string;
//   location: string;
//   registered?: boolean
//   inPlan? : boolean
// }

// const coursePlaceholders = {
//   "CSE 30332": {
//     name: "Programming Paradigms",
//     professor: "Joanna Cecilia da Silva Santos",
//     time: "2:00PM-3:15PM",
//     dates: "MW",
//     location: "DeBartolo Hall 126",
//     inPlan: false
//   },
//   "CSE 40113": {
//     name: "Design/Analysis of Algorithms",
//     professor: "Erin Chambers",
//     time: "10:30AM-11:20AM",
//     dates: "MWF",
//     location: "Cushing Hall of Engineering 303",
//     inPlan: false
//   },
// }
//course.professor[0] + ". " + course.professor.split(" ")[course.professor.split(" ").length - 1]

const searchEntered = ref<boolean>(false);

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100..900&family=Roboto:wght@100..900&display=swap');

.search-container {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
  min-height: 100vh;
  padding-bottom: 80px; /* Controls distance from bottom */
}

.search-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.search-title {
  font-size: 24px;
  font-weight: 600;
  color: #4A3D00;
  margin-bottom: 16px;
}

.search-box {
  width: 600px;
  height: 150px;
  padding: 16px;
  border: 1px solid #ccc;
  border-radius: 8px;
  resize: none;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  font-size: 16px;
  outline: none;
  margin-bottom: 128px;
  font-size: 16px;
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
}
</style>