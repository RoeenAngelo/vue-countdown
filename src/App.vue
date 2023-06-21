<script setup>
import { computed, reactive, ref } from 'vue';
import { RouterLink, RouterView } from 'vue-router'
import Event from './components/Event.vue';
import AddUpdateForm from './components/AddUpdateForm.vue';

const eventData = reactive([
  {
    id: 1,
    name: "Graduation",
    details: "wooohoo!!!",
    date: "2022-09-25",
    background: "#F34949",
  },
  {
    id: 2,
    name: "Holidays",
    details: "wooohoo!!!",
    date: "2028-10-02",
    background: "#f9f970",
  },
  {
    id: 3,
    name: "HolidayYYYY",
    details: "Get me outta here!",
    date: "2023-06-18",
    background: "#7AD3F0",
  },
  {
    id: 4,
    name: "Birthday",
    details: "My birthday party",
    date: "2023-06-17",
    background: "#F07AEC",
  },
  {
    id: 5,
    name: "Christmas",
    details: "ho ho ho",
    date: "2023-06-19",
    background: "#EB9A0F",
  },
  { 
    id: 6,
    name: "Conference Talk",
    details: "dont flop",
    date: "2026-02-28",
    background: "#68EE94",
  },
]);


const showPastEvents = ref(false)
let showForm = ref(false)

function daysLeft(event) {
      const time = Date.parse(event.date) - Date.now();
      const days = Math.ceil(time / (1000 * 3600 * 24));
      return days;
    }

const orderEvents = computed(() => {
  const eventsToOrder = eventData
  return eventsToOrder.sort((a,b) => a.date > b.date ? 1 : -1)
})

function addNewEvent(event) {
  event.id = eventData.length + 1
  eventData.push(event)
}


</script>

<template>
  <teleport to="#modal">
    <AddUpdateForm 
    @close-form="showForm = false"
    @add-new-event="addNewEvent($event)"
    v-if="showForm" 
    />
  </teleport>

  <div class="options">
    <button @click="showPastEvents = !showPastEvents">Show Past Events</button>
    <button class="addNew" @click="showForm = !showForm">&#43;</button>
  </div>
  <ul>
    <li
    v-for="event in orderEvents" 
		:key="event.id"
		>
      <Event 
      :event="event"
      :daysLeft="daysLeft(event)"
      :showPastEvents="showPastEvents"
      />
    </li>
  </ul>
</template>

<style >

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
}

ul {
  padding: 0;
}

li {
  list-style: none;
  cursor: pointer;
}
</style>
