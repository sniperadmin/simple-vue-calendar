<template>
  <div id="calendar-entry">
    <div class="calendar-entry-note">
      <input v-model="entry" type="text" placeholder="New Event" />
      <p class="calendar-entry-day">
        Day of event: <span class="bold">{{ activeDay }}</span>
      </p>
      <a @click="submitEvent(entry)" class="button is-primary is-small is-outlined">Submit</a>
    </div>
    <p style="color: red; font-size: 13px" v-if="error">
      You must type something first!
    </p>
  </div>
</template>

<script>
  import { store } from "../store";
  export default {
    name: 'CalendarEntry',
    data() {
      return {
        entry: '',
        error: false
      }
    },
    methods: {
      submitEvent (eventDetails) {
        if (!eventDetails || eventDetails === '') {
          return this.error = true
        }
        store.submitEvent(eventDetails)
        this.entry = ''
        this.error = false
      }
    },
    computed: {
      activeDay () {
        return store.getActiveDay().fullTitle
      }
    },
  }
</script>

<style lang="scss" scoped>
#calendar-entry {
  background: #FFF;
  border: 1px solid #42b883;
  border-radius: 10px;
  max-width: 300px;
  margin: 0 auto;
  padding: 20px;

  .calendar-entry-note {
    input {
      width: 200px;
      font-weight: 600;
      border: 0;
      border-bottom: 1px solid #CCC;
      font-size: 15px;
      height: 30px;
      margin-bottom: 10px;

      &:focus {
        outline: none;
      }
    }

    .calendar-entry-day {
      color: #42b883;
      font-size: 12px;
      margin-bottom: 10px;
      padding-bottom: 5px;

      .bold {
        font-weight: 600;
      }
    }

    .submit {
      display: block;
      margin: 0 auto;
    }
  }
}
</style>