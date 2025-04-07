<template>
  <div class="search-container" v-if="!searchEntered">
    <h2 class="search-title">What are you searching for?</h2>
    <textarea class="search-box" placeholder="Ask anything..." @keyup="displayResults"></textarea>
  </div>
  <div class="search-entered" v-if="searchEntered">
    <p class="search-text">
      Sure! Here are some of the typical classes for the sophomore fall semester of computer science students:
    </p>

    <div class="course-card">
      <p class="course-number">1. <i><u>CSE 20221 Logic Design and Sequential Circuits</u></i></p>
      <p><strong>Time:</strong> TTh 9:30 AM - 10:45 AM</p>
      <p><strong>Professor:</strong> A. Dingler</p>
      <button class="info-button">More Info</button>
      <span class="requirement-tag">CSE Requirement</span>
    </div>
  </div>
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
//   "CSE 40175": {
//     name: "Ethical and Professional Issues",
//     professor: "Kevin Bowyer",
//     time: "11:00AM-12:15PM",
//     dates: "TR",
//     location: "Jordon Hall of Science 105",
//     inPlan: false
//   },
//}
//course.professor[0] + ". " + course.professor.split(" ")[course.professor.split(" ").length - 1]

const searchEntered = ref<boolean>(false);
const displayResults = (event: KeyboardEvent) => {
  console.log(event.key)
  if (event.key === "Enter") {
    searchEntered.value = true;
  }
}

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100..900&family=Roboto:wght@100..900&display=swap');

.search-container {
  /*padding-top: 50px; */
  margin-top: 450px;
  margin-left: auto;
  margin-right: auto;
  width: 1000px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
  background-color: #002349;
  border-radius: 10px;
}

.search-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.search-title {
  font-size: 24px;
  font-weight: 600;
  color: #fbbf24;
}

.search-box {
  width: 800px;
  height: 20px;
  padding: 16px;
  border: 2px solid #807e7e;
  border-radius: 20px;
  resize: none;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  font-size: 16px;
  outline: none;
  font-size: 16px;
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
  margin-bottom: 1.5em;
}

.search-entered {
  margin-top: 50px;
  margin-left: auto;
  margin-right: auto;
  width: 1000px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
  background-color: #002349;
  border-radius: 10px;
}

.search-text {
  font-size: 18px;
  margin-bottom: 20px;
}

.course-card {
  margin-bottom: 30px;
  border-bottom: 1px solid #ccc;
  padding-bottom: 20px;
  position: relative;
}

.course-number {
  font-weight: bold;
  font-size: 16px;
  margin-bottom: 8px;
}

.info-button {
  background-color: #d3d3d3;
  border: none;
  padding: 8px 16px;
  font-weight: bold;
  margin-top: 10px;
  cursor: pointer;
}

.requirement-tag {
  position: absolute;
  right: 0;
  top: 0;
  font-weight: bold;
  color: #594800;
}

.theo-philo-grid {
  display: flex;
  gap: 40px;
  margin-top: 10px;
}

.column p {
  margin: 8px 0;
}

.search-icon {
  font-size: 18px;
  margin-left: 10px;
  border: 1px solid black;
  background-color: transparent;
  cursor: pointer;
  padding: 2px 6px;
  border-radius: 2px;
}

</style>