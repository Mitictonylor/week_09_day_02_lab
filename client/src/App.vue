<template lang="html">
  <div>
    <div class="menu-bar-container">
      <div class="menu-bar">
      <div class="logo-container">
        <img class="logo" src="./assets/logo.png" alt="">
      </div>
      <div class="title-container">
        <p class="title">Hotel Bookings</p>
      </div>
    </div>
    </div>
    <booking-form></booking-form>
    <booking-list :bookings="bookings"></booking-list>
  </div>
</template>

<script>
import BookingForm from '@/components/BookingForm';
import BookingList from '@/components/BookingList';
import BookingService from '@/services/BookingService';
import {eventBus} from '@/main.js';

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
    this.getBooking();

    eventBus.$on('booking-added', (booking) => {
      this.bookings.push(booking);
    });

    eventBus.$on('booking-updated', (updatedBooking) => {
      let index = this.bookings.findIndex(booking => booking._id === updatedBooking._id);
      this.bookings.splice(index, 1, updatedBooking);
    });

    eventBus.$on('booking-deleted', (id) => {
      let index = this.bookings.findIndex(booking => booking._id === id);
      this.bookings.splice(index, 1);
    })

  },
  methods: {
    getBooking(){
      BookingService.getBooking()
      .then(bookings => this.bookings = bookings)
    }
  }
}
</script>

<style lang="css" scoped>
.title {
  font-size: 50px;
  color: #cb997e;
  font-family: 'Open Sans', sans-serif;
}

@media screen and (max-width: 730px) {
  .title {
    font-size: 80px;
  }
}
.logo-container {
  width: 15%;
  float: left;
    border-style: solid;
}
.logo {
  height: 50px;
  margin-top: 7px;
  margin-bottom: 7px;
}
.title-container {
  width: 75%;
  float: left;
  border-style: solid;
}
.menu-bar-container {
  border-style: solid;
  overflow: auto;
  display: block;
  text-align: center;
}
.menu-bar {
  border-style: solid;
  overflow: auto;
  display: inline-block;
  text-align: center;
  width: 42%;
}
</style>

<style>
body {
  /* background-image: url('assets/background.png');
  background-position: center;
  background-size: cover;
  background-attachment: fixed;
  cursor: url('assets/cursor.png'), auto; */
  user-select: none;
}
p {
  padding: 0;
  margin: 0;
}

</style>
