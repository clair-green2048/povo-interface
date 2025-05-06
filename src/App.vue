<template>
  <div class="page">
    <HomePage v-if="currentPage === 'HomePage'" 
      @toggle-page="togglePage"
    ></HomePage>
    <TabsBar 
      v-if="currentPage != 'HomePage'" 
      :openTabs="openTabs"
      :currentTab="currentTab"
      @toggle-page="togglePage"
      @close-tab="closeTab">
    </TabsBar>
    <PlansPage v-if="currentPage === 'CoursePlansPage'" 
      :coursePlans="coursePlans"
      :currentPlan="currentPlan"
      @select-plan="selectPlan"
      @create-new-plan="createNewPlan"
      @toggle-page="togglePage"
      @drop-courses="dropCourses">
    </PlansPage>
    <RegistrationPage v-if="currentPage === 'CourseRegistrationPage'"
      :coursePlans="coursePlans"
      :currentPlan="currentPlan"
      :registeredCourses="registeredCourses"
      @select-plan="selectPlan"
      @register-courses="registerCourses"
      @drop-courses="dropCourses"
      @toggle-page="togglePage">
    </RegistrationPage>
    <SchedulePage v-if="currentPage === 'SchedulePage'"
      :coursePlans="coursePlans"
      :currentPlan="currentPlan"
      @select-plan="selectPlan">
    </SchedulePage>
    <SearchPage v-if="currentPage === 'SearchPage'"
      :coursePlans="coursePlans"
      :currentPlan="currentPlan"
      @add-course="addCourse"
      @drop-course="dropCourse"
      @select-plan="selectPlan">
    </SearchPage>
  </div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import HomePage from './components/HomePage.vue';
import TabsBar from './components/TabsBar.vue';
import PlansPage from './components/PlansPage.vue';
import RegistrationPage from './components/RegistrationPage.vue';
import SchedulePage from './components/SchedulePage.vue';
import SearchPage from './components/SearchPage.vue';

// ### TABS BAR ###
const currentPage = ref<string>("HomePage");
const openTabs = ref<Array<string>>(["CoursePlansPage", "CourseRegistrationPage", "SchedulePage", "SearchPage"]);
const currentTab = ref<string>("");

const togglePage = (pageName: string) => {
  if (pageName) {
    currentPage.value = pageName;
    if (pageName != "HomePage") {
      currentTab.value = pageName
      openTabs.value = ["CoursePlansPage", "CourseRegistrationPage", "SchedulePage", "SearchPage"]
    }
    else {
      openTabs.value = []
    }
  }
}

const closeTab = (tabName: string) => {
  openTabs.value = openTabs.value.filter(tab => tab !== tabName);
  if (openTabs.value.length === 0) {
    currentTab.value = ""
    currentPage.value = "HomePage"
  }
  if (tabName === currentTab.value) {
    currentTab.value = openTabs.value[openTabs.value.length - 1]
    currentPage.value = currentTab.value
  }
}

// ### PLANS ###
interface Course {
  name: string;
  professor: string;
  time: string;
  dates: string;
  credits: string;
  location: string;
  requirements: string;
  description: string
  registered?: boolean
  inPlan? : boolean,
}

const coursePlans = ref<Record<string, Record<string, Course>>>({
  "Heavy CS": {
    "CSE 30311": {
      name: "Theory of Computing",
      professor: "David Chiang",
      time: "2:00PM-3:15PM",
      dates: "TR",
      location: "DeBartolo Hall 126",
      credits: "3",
      requirements: "CSE Major Requirement",
      description: "Introduction to formal languages and automata, computability theory, and complexity theory with the goal of developing understanding of the power and limits of different computational models. Topics covered include: regular languages and finite automata; context-free grammars and pushdown automata; Turing machines; undecidable languages; the classes P and NP; NP completeness",
      inPlan: true,
    },
    "CSE 30124": {
      name: "Introduction to Artificial Intelligence",
      professor: "William Theisen",
      time: "2:00PM-3:15PM",
      dates: "MW",
      location: "DeBartolo Hall 155",
      credits: "3",
      requirements: "CSE Elective",
      description: "Foundational concepts and techniques in AI and machine learning. Historical overview of the field. Search and logic programming. Canonical machine learning tasks and algorithms: supervised and unsupervised learning (classification and regression). Essential concepts from probability and statistics relevant to machine learning. Performance characterization. Modern software environments for machine learning and AI programming. Applications in unsupervised and supervised learning from image and textual data.",
      inPlan: true,
    }
  },
  "Major Reqs": {
    "CSE 30311": {
      name: "Theory of Computing",
      professor: "David Chiang",
      time: "2:00PM-3:15PM",
      dates: "TR",
      location: "DeBartolo Hall 126",
      inPlan: true,
      credits: "3",
      requirements: "CSE Major Requirement",
      description: "Introduction to formal languages and automata, computability theory, and complexity theory with the goal of developing understanding of the power and limits of different computational models. Topics covered include: regular languages and finite automata; context-free grammars and pushdown automata; Turing machines; undecidable languages; the classes P and NP; NP completeness"
    },
    "CSE 30341": {
      name: "Operating System Principles",
      professor: "Douglas Thain",
      time: "9:30AM-10:45AM",
      dates: "TR",
      location: "Pasquerilla Center 107",
      inPlan: true,
      credits: "3",
      requirements: "CSE Major Requirement",
      description: "Introduction to all aspects of modern operating systems. Topics include process structure and synchronization, interprocess communication, memory management, file systems, security, I/O, and distributed files systems"
    },
    "MATH 30750": {
      name: "Real Analysis",
      professor: "Qing Han",
      time: "9:25AM-10:15AM",
      dates: "MWF",
      location: "Riley Hall 200",
      inPlan: true,
      credits: "3",
      requirements: "CHEM Elective, WKQR Core Quantitative Reasoning",
      description: "A rigorous treatment of differential and integral calculus. Topics include a review of sequences and continuity, differentiability, Taylor's theorem, integration, the fundamental theorem of Calculus, pointwise and uniform convergence, and power series. Additional topics are likely and will depend on the instructor. Emphasis throughout will be on careful mathematical definitions and thorough understanding of basic results"
    }
  }
})

const currentPlan = ref<string>("Heavy CS");

const selectPlan = (planName: string) => {
  currentPlan.value = planName;
}

const createNewPlan = (planName: string) => {
  coursePlans.value[planName] = {}
  selectPlan(planName)
}

const dropCourses = (planName: string, courseNumbers: Array<string>) => {
  for (const courseNumber of courseNumbers) {
    delete coursePlans.value[planName][courseNumber];
  }
}

// ### REGISTRATION ###
const registeredCourses = ref<Record<string, Course>>({})
const registerCourses = (planName: string, courseNumbers: Array<string>) => {
  for (const courseNumber of courseNumbers) {
    coursePlans.value[planName][courseNumber].registered = true;
    registeredCourses.value[courseNumber] = coursePlans.value[planName][courseNumber]
  }
  currentPlan.value = planName;
}

// ### SEARCH ###
const addCourse = (planName: string, number: string, course: Course) => {
  course.inPlan = true
  coursePlans.value[planName][number] = course;
}

const dropCourse = (planName: string, number: string) => {
  delete coursePlans.value[planName][number]
  console.log(coursePlans.value[planName]);
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50; 
  min-height: 100vh;
}

html, body {
  height: 100%;
  margin: 0px;
  padding: 0;
}
body { 
  /*background-image: url('./assets/background.png'); */
  background-size: cover;        
  background-position: center;   
  background-repeat: no-repeat;
  background-attachment: fixed;
  overflow: hidden;
}
</style>
