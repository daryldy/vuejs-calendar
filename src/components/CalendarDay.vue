<template>
  <div :class="classObject">
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
    }
  }
</script>
