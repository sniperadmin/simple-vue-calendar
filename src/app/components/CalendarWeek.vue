<template>
  <div id="calendar-week" class="container">
      <div class="columns is-mobile">
        <CalendarDay
          v-for="day in sharedState.seedData"
          :key="day.id"
          :day="day"
        />
      </div>
    </div>
</template>

<script>
import { store } from '../store'
import CalendarDay from "../components/CalendarDay";

  export default {
    name: 'CalendarWeek',
    components: {
      CalendarDay,
    },
    data() {
      return {
        sharedState: store.state
      }
    },
  }
</script>

<style lang="scss">
#calendar-week {
  margin-bottom: 50px;
  .column {
    padding: 0 0 0 0;
  }
}
</style>