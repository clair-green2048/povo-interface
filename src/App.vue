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
      @select-plan="selectPlan">
    </PlansPage>
    <RegistrationPage v-if="currentPage === 'CourseRegistrationPage'"
      :coursePlans="coursePlans"
      :currentPlan="currentPlan"
      @register-courses="registerCourses"
      @drop-courses="dropCourses">
    </RegistrationPage>
    <SchedulePage v-if="currentPage === 'SchedulePage'"></SchedulePage>
    <SearchPage v-if="currentPage === 'SearchPage'"></SearchPage>
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
const openTabs = ref<Array<string>>([]);
const currentTab = ref<string>("");

const togglePage = (pageName: string) => {
  if (pageName) {
    currentPage.value = pageName;
    if (pageName != "HomePage") {
      currentTab.value = pageName
      if (!openTabs.value.includes(currentTab.value)) {
        openTabs.value.push(currentTab.value)
      }
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
  location: string;
  registered?: boolean
  inPlan? : boolean
}

const coursePlans = ref<Record<string, Record<string, Course>>>({
  "Heavy CS": {
    "CSE 30311": {
      name: "Theory of Computing",
      professor: "David Chiang",
      time: "2:00PM-3:15PM",
      dates: "TTh",
      location: "DeBartolo Hall 126",
      inPlan: true
    },
    "CSE 30124": {
      name: "Introduction to Artificial Intelligence",
      professor: "William Theisen",
      time: "3:30PM-4-45PM",
      dates: "MW",
      location: "DeBartolo Hall 155",
      inPlan: true
    }
  },
  "Major Reqs": {
    "CSE 30311": {
      name: "Theory of Computing",
      professor: "David Chiang",
      time: "2:00PM-3:15PM",
      dates: "TTh",
      location: "DeBartolo Hall 126",
      inPlan: true
    },
    "CSE 30341": {
      name: "Operating System Principles",
      professor: "Douglas Thain",
      time: "9:30AM-10:45AM",
      dates: "TTh",
      location: "Pasquerilla Center 107",
      inPlan: true
    },
    "MATH 30750": {
      name: "Real Analysis",
      professor: "Qing Han",
      time: "9:25AM-10:15AM",
      dates: "MWF",
      location: "Riley Hall 200",
      inPlan: true
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

const dropCourses = (planName: string, courseNumbers: Array<string>, removeFromPlan: boolean) => {
  if (removeFromPlan) {
    for (const courseNumber of courseNumbers) {
      delete coursePlans.value[planName][courseNumber];
    }
  }
  else {
    for (const courseNumber of courseNumbers) {
      coursePlans.value[planName][courseNumber].registered = false;
    }
  }
}

// ### REGISTRATION ###
const registerCourses = (planName: string, courseNumbers: Array<string>) => {
  for (const courseNumber in courseNumbers) {
    coursePlans.value[planName][courseNumber].registered = true;
  }
  currentPlan.value = planName;
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
  background-image: url('./assets/background.png');
  background-size: cover;        /* make it fill the screen */
  background-position: center;   /* center the image */
  background-repeat: no-repeat;
  background-attachment: fixed;
  overflow: hidden;
}
</style>