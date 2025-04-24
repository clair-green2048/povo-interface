<template>
  <div class="tabs-bar">
    <img src="../assets/ndlogo.png" @click="emit('toggle-page', 'HomePage')">
    <BaseTab v-for="tab in props.openTabs" 
      :key="tab" 
      :tabName="tab" 
      :isSelected="tab === props.currentTab"
      @select-tab="togglePage">
    </BaseTab>
    <!-- <button class="add-tab" :class="{ active: addTab === true }" ref="addTabRef" @click="addTab = !addTab">+</button> -->
  </div>
  <!-- <div class="add-tab-menu" ref="addTabMenuRef" v-if="addTab === true" >
    <div v-for="tab in unopenedTabs"
    :key="tab"
    class="add-tab-option"
    @click="toggleNewTab(tab)">
      {{ formatTabName(tab) }}
    </div>
  </div> -->
</template>

<script lang="ts" setup>
import { defineProps, defineEmits } from 'vue'
import BaseTab from '../global/BaseTab.vue'

interface Props {
  openTabs: Array<string>
  currentTab: string
}
const props = defineProps<Props>();
const emit = defineEmits(["toggle-page", "close-tab"])

const togglePage = (tabName: string) => {
  emit("toggle-page", tabName)
}

// const closeTab = (tabName: string) => {
//   emit("close-tab", tabName)
// }

// const addTab = ref<boolean>(false)
// const availableTabs = ["CoursePlansPage", "CourseRegistrationPage", "SchedulePage", "SearchPage"];
// const unopenedTabs = computed(() => {
//   const tabs: string[] = []
//   for (let i = 0; i < availableTabs.length; i++) {
//     if (!props.openTabs.includes(availableTabs[i])) {
//       tabs.push(availableTabs[i]);
//     }
//   }
//   return tabs
// })

// const addTabRef = ref<HTMLElement | null>(null)
// const addTabMenuRef = ref<HTMLElement | null>(null)

// const handleOutsideClick = (event: MouseEvent) => {
//   if (addTabMenuRef.value && !addTabMenuRef.value.contains(event.target as Node) && !addTabRef.value.contains(event.target as Node)) {
//     addTab.value = false;
//   }
// }

// onMounted(() => {
//   document.addEventListener("click", handleOutsideClick)
// })

// onUnmounted(() => {
//   document.removeEventListener("click", handleOutsideClick);
// })

// const toggleNewTab = (tabName: string) => {
//   addTab.value = !addTab.value;
//   emit("toggle-page", tabName)
// }

// const formatTabName = (tabName: string) => {
//   return tabName.replace('Page', '').replace(/([a-z])([A-Z])/g, '$1 $2')
// }

</script>

<style scoped>
img {
  width: 60px;
  height: 60px;
  cursor: pointer;
  border-right: 2px solid black;
  flex-shrink: 0;
}

.tabs-bar {
  display: flex;
  border: 1px solid black;
  align-items: stretch;
  width: 100%;
}

.tab {
  display: flex;
  text-align: center;
  justify-content: center;
  align-items: center;
  width: 100%;
  font-family: 'Roboto', sans-serif;
  font-size: 24px;
  color: black;
}

.add-tab {
  height: 60px;
  width:60px;
  flex-shrink: 0;
  border: 2px solid black;
  background-color: #fef6ff; 
  color: #2c2c2c;
  font-size: 16px;
  font-weight: bold;
  text-align: center;
  cursor: pointer;
  transition: background-color 0.2s ease, font-weight 0.2s ease;
}

.add-tab:hover {
  background-color: #f0e6ff;
}

.active {
  border-bottom: 2px solid transparent;
}
.add-tab-menu {
  position: absolute;
  top: 62px;
  right: 0px;
  background: white;
  border: 1px solid #ccc;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  z-index: 10;
  min-width: 180px;
  font-family: 'Roboto', sans-serif;
}

.add-tab-option {
  padding: 10px 16px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.add-tab-option:hover {
  background-color: #f0e6ff;
}
</style>