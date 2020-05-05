<template lang="html">
  <div>
    <p class="title">Hotel Bookings</p>
    <booking-form></booking-form>
    <booking-list :bookings="bookings"><booking-list>
  </div>
</template>

<script>
import BookingForm from '@/components/BookingForm.vue';
import BookingList from '@/components/BookingList.vue';

export default {
  name: 'App',
  data(){
    return{
      bookings: [],
      newBooking: null
    }
  },
  components: {
    "booking-form": BookingForm,
    "booking-list": BookingList,
  },
  mounted() {
    this.getBookings();

    eventBus.$on('booking-added', (booking) => {
      this.bookings.push(booking);
    });
    
  },
  methods: {
    getBookings(){
      BookingService.getBookings()
      .then(bookings => this.bookings = bookings)
    }
  }
}
</script>

<style lang="css" scoped>
.title {
  font-size: 100px;
}
</style>

<style>
p {
  padding: 0;
  margin: 0;
}
</style>
