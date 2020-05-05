<template lang="html">
  <form class="" v-on:submit.prevent="addBooking" method="post">
    <label for="name">Name:</label>
    <input type="text" v-model="name" required/>
    <label for="email">Email:</label>
    <input type="text" v-model="email" required/>
    <input type="hidden" v-model="status" value="false" hidden/>
    <input type="submit" value="Save"/>
  </form>
</template>

<script>
import BookingService from '@/services/BookingService';
import {eventBus} from '@/main.js';

export default {
  name: 'booking-form',
  data() {
    return {
      name: '',
      email: '',
      status: ''
    }
  },
  methods: {
    addBooking(event) {
      const newBooking = {
        name: this.name,
        email: this.email,
        status: this.status
      }
      BookingService.addBooking(newBooking)
      .then(booking => eventBus.$emit('booking-added', booking))
    }
  }
}
</script>

<style lang="css" scoped>
</style>
