<template>
  <div class="day-event" :style="getEventBackgroundColor">
    <div v-if="!event.edit">
      <span class="has-text-centered details">{{ event.details }}</span> 
      <div class="has-text-centered icons">
        <i @click="editEvent(dayId, event.details)" class="fa fa-pencil-square edit-icon fa-lg"></i> 
        <i
          @click="deleteEvent(dayId, event.details)"
          class="fa fa-trash-o delete-icon fa-lg"
        ></i>
      </div>
    </div>
    <div v-else>
      <input v-model="newEventDetails" type="text" :placeholder="event.details" />
      <div class="has-text-centered icons">
        <i
          @click="updateEvent(dayId, event.details, newEventDetails)"
          class="fa fa-check"
        ></i>
      </div>
    </div>
  </div>
</template>

<script>
import { store } from "../store";
  export default {
    name: 'CalendarEvent',
    props: {
      event: {
        type: Object,
        default: null,
      },
      dayId: {
        type: Number,
        default: null,
      },
    },
    data() {
      return {
        newEventDetails: ''
      }
    },
    methods: {
      editEvent(dayId, eventDetails) {
        store.editEvent(dayId, eventDetails)
      },
      updateEvent(dayId, originalEventDetails, updatedEventDetails) {
        if (updatedEventDetails === '') updatedEventDetails = originalEventDetails
        store.updateEvent(dayId, originalEventDetails, updatedEventDetails)
        this.newEventDetails = ''
      },
      deleteEvent(dayId, eventDetails) {
        store.deleteEvent(dayId, eventDetails)
      }
    },
    computed: {
      getEventBackgroundColor () {
        const colors= ['#FF9999', '#85D6FF', '#99FF99']
        let randomColor = colors[Math.floor(Math.random() * colors.length)]
        return `background-color: ${randomColor}`
      }
    },
  }
</script>

<style lang="scss" scoped>

</style>