<template lang="html">
  <div class="booking">
    <p>Name: {{booking.name}}</p>
    <p>Email: {{booking.email}}</p>
    <button class="tooltip"v-if="!booking.status"type="button" v-on:click="updateBooking"><img src="@/assets/checkin.png" class="check-in"><span class="tooltiptext">Check In</span></button>
    <button class="tooltip"type="button" v-on:click="deleteBooking"><img src="@/assets/delete.png" class="delete"><span class="tooltiptext">Delete</span></button>
  </div>
</template>

<script>
import {eventBus} from '@/main.js'
import BookingService from '@/services/BookingService'

export default {
  name: 'booking-list-item',
  props: ['booking'],
  methods: {
    updateBooking() {
      const updateBooking = {status: true}
      BookingService.updateBooking(this.booking._id, updateBooking)
      .then((booking) => eventBus.$emit('booking-updated', booking))
    },
    deleteBooking() {
      BookingService.deleteBooking(this.booking._id)
      .then(() => eventBus.$emit('booking-deleted', this.booking._id))
    }
  }
}
</script>

<style lang="css" scoped>
.booking{
  border-color: #f1e2cc;
  border-style: solid;
  width: 200px;
  float: left;
  margin: 5px;
}

@media screen and (max-width: 600px) {
  .booking {
    border-style: solid;
    width: 400px;
  }
}
.delete{
margin: 0;
padding: 0;
width: 16px;
height: 16px;
}
.check-in{
  margin: 0;
  padding: 0;
  width: 16px;
  height: 16px
}
.delete:hover{
  opacity:50%
}
.check-in:hover{
  opacity:50%
}
button{
  background: transparent;
  border: none
}
.tooltip {
  position: relative;
  display: inline-block;
  border-bottom: 0px ;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 60px;
  background-color: #f1e2cc;
  color: #794D3F;
  text-align: center;
  border-radius: 6px;
  padding: 5px 0;
  position: absolute;
  z-index: 1;
  top: 100%;
  left: 50%;
  right:50%;
  margin-left: -30px;

  /* Fade in tooltip - takes 1 second to go from 0% to 100% opac: */
  opacity: 0;
  transition: opacity 1s;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;}
</style>
