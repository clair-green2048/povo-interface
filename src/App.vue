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
    <PlansPage v-if="currentPage === 'CoursePlansPage'"></PlansPage>
    <RegistrationPage v-if="currentPage === 'CourseRegistrationPage'"></RegistrationPage>
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