<template>
  <div class="calendar">
    <vue-cal
      :hideWeekends="true"
      :views-bar="false"
      :title-bar="false" 
      :time-from="8 * 60"
      :time-to="19 * 60"
      :events="courseEvents">
      <template #time-cell="{ format12 }">
        <strong>{{ format12 }}</strong>
      </template>
      <template #weekday-heading="{ label, id }">
        <strong :class="id">{{ label }}</strong>
      </template>
      <template #event="{ event }">
        <div class="custom-event">
          <strong class="event-title">{{ event.title }}</strong>
          <div class="event-time">{{ formatDate(event.start, event.end) }}</div>
          <div class="event-content">{{ event.content.split(" ")[0] + " " + event.content.split(" ")[event.content.split(" ").length - 1] }}</div>
        </div>
      </template>
    </vue-cal>
  </div>
</template>

<script lang="ts" setup>
//@ts-ignore
import { VueCal } from 'vue-cal'
import 'vue-cal/style'
import { defineProps, computed } from 'vue'


interface Props {
  coursePlans: Record<string, Record<string, Course>>;
  currentPlan: string;
}
const props = defineProps<Props>();

interface Course {
  name: string;
  professor: string;
  time: string;
  dates: string;
  location: string;
  registered?: boolean;
  inPlan? : boolean;
}

const dayToDate: Record<string, string> = {
  "M": '2025-04-07',
  "T": '2025-04-08',
  "W": '2025-04-09',
  "R": '2025-04-10',
  "F": '2025-04-11',
}

const parseTimeRange = (timeRange: string) => {
  const convert = (time: string) => {
    time = time.replace(/(AM|PM)/, ' $1')
    let [hourStr, minutePart] = time.trim().split(":");
    console.log(hourStr)
    console.log(minutePart)
    let minute = minutePart.slice(0, 2);
    const isPM = time.includes("PM");
    let hour = Number(hourStr);

    if (isPM && hour !== 12) hour += 12;
    if (!isPM && hour === 12) hour = 0;

    return `${hour.toString().padStart(2, "0")}:${minute}`;
  };

  const [startRaw, endRaw] = timeRange.split("-");
  const start = convert(startRaw);
  const end = convert(endRaw);

  return { start, end };
};

const formatDate = (start: Date, end: Date) => {
  const options: Intl.DateTimeFormatOptions = {
    hour: 'numeric',
    minute: '2-digit',
    hour12: true
  };

  const startStr = start.toLocaleTimeString([], options);
  const endStr = end.toLocaleTimeString([], options);

  return `${startStr} - ${endStr}`;
};

const courseEvents = computed(() => {
  const plan = props.coursePlans[props.currentPlan];
  const events = [];

  for (const courseNumber in plan) {
    const course = plan[courseNumber];
    const { start, end } =  parseTimeRange(course.time);

    for (let i = 0; i < course.dates.length; i++) {
      const date = dayToDate[course.dates[i]];

      if (date) {
        events.push({
          title: `${course.name}`,
          start: new Date(`${date}T${start}`),
          end: new Date(`${date}T${end}`),
          content: `${course.location}`,
          class: "event",
          background: true
        })
      }
      console.log("Start:", start, "End:", end, "Full:", `${date}T${start}`);
    }
  }

  return events;
})

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@100..900&family=Roboto:wght@100..900&display=swap');

.vuecal {
  --vuecal-height: 800px;
  --vuecal-secondary-color:#002349;
  --vuecal-event-color: #ffffff;
  --vuecal-base-color: #fbbf24;
  --vuecal-primary-color: #00843d;
  --vuecal-border-radius: 0px;
  cursor: default;
  font-family: Montserrat, sans-serif;
  font-weight: 700;
}

.vuecal__time-column {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}


.custom-event {
  font-family: Roboto, sans-serif;
  font-weight: 400;
  font-size: 12px;
  display: flex;
  height: 100%;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.event-time {
  margin-top: 4px;
  margin-bottom: 2px; 
}

.custom-cell {
  background-color: #ffffff;
}



</style>