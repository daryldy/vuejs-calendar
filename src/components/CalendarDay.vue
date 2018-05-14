<template>
  <div :class="classObject" @click="captureClick">
    {{ day.format('D') }}
    <ul class="event-list">
      <li v-for="event in events">{{ event.description }}</li>
    </ul>
  </div>
</template>
<script>
  export default {
    props: [ 'day' ],
    computed: {
      events() {
        return this.$store.state.events.filter(event => event.date.isSame(this.day, 'day'))
      },
      classObject() {
        let eventFormDate = this.$store.state.eventFormDate
        let eventFormActive = this.$store.state.eventFormActive
        let today = this.$moment()
        let isToday = this.day.isSame(today, 'day')
        return {
          day: true,
          today: isToday,
          past: this.day.isSameOrBefore(today, 'day') && ! isToday,
          active: eventFormDate.isSame(this.day,'day') && eventFormActive
        }
      }
    },
    methods: {
      captureClick(event) {
        this.$store.commit('eventFormPos', { x: event.clientX, y: event.clientY })
        this.$store.commit('eventFormActive', true)
        this.$store.commit('eventFormDate', this.day)
      },
    },
  }
</script>
