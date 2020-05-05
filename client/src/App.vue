<template lang="html">
  <div>
    <p class="title">Hotel Bookings</p>
    <booking-form></booking-form>
    <booking-list :bookings="bookings"><booking-list>
  </div>
</template>

<script>
import BookingForm from '@/components/BookingForm';
import BookingList from '@/components/BookingList';
import BookingService from '@/components/BookingService';

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

    eventBus.$on('booking-updated', (updatedBooking) => {
      let index = this.bookings.findIndex(booking => booking._id === updatedBooking._id);
      this.bookings.splice(index, 1 updatedBooking);
    });

    eventBus.$on('booking-deleted', (id) => {
      let index = this.bookings.findIndex(booking => booking._id === id);
      this.bookings.splice(index, 1);
    })

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
