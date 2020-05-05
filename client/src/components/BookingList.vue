<template lang="html">
  <booking-list-item v-for="booking in bookings" :booking="booking"></booking-list-item>
</template>

<script>
import BookingListItem from '@/components/BookingListItem'
import BookingService from '@/services/BookingService'

export default {
  name: 'booking-list',
  props: ['bookings'],
  components: {
    'booking-list-item': BookingListItem
  }
}
</script>

<style lang="css" scoped>
</style>
