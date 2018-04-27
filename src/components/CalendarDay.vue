<template>
  <div :class="classObject" @click="captureClick">
    {{ day.format('D') }}
  </div>
</template>
<script>
  export default {
    props: [ 'day' ],
    computed: {
      classObject() {
        let today = this.$moment()
        let isToday = this.day.isSame(today, 'day')
        return {
          day: true,
          today: isToday,
          past: this.day.isSameOrBefore(today, 'day') && ! isToday
        }
      }
    },
    methods: {
      captureClick(event) {
        this.$store.commit('eventFormPos', { x: event.clientX, y: event.clientY })
      },
    },
  }
</script>
