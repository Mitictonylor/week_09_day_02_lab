<template lang="html">
  <div class="form-container">
    <form class="form" v-on:submit.prevent="addBooking" method="post">
      <div class="name">
        <label for="name">Name:</label>
        <input type="text" v-model="name" placeholder="           Insert name" required/>
      </div>
      <div class="email">
        <label for="email">Email:</label>
        <input type="text" v-model="email" placeholder="    Insert email address" required/>
      </div>
      <div class="status">
        <input type="hidden" v-model="status" value="false" hidden/>
        <input class="save" type="image" :src="save" value="Save"></input>
      </div>
    </form>
  </div>
</template>

<script>
import BookingService from '@/services/BookingService';
import {eventBus} from '@/main.js';
import save from '@/assets/save.png';

export default {
  name: 'booking-form',
  data() {
    return {
      name: '',
      email: '',
      status: '',
      save: save
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
    },
  }
}
</script>

<style lang="css" scoped>
.form-container {
  display: block;
  text-align: center;

background-color: #fff1e6;
}
.form {
  border-color: #f1e2cc;
  border-style: solid;
  display: inline-block;
  width: 25%;
  margin: 10px;
background-color: #fff1e6;


}
.name {
  margin: 10px;
}
.email {
  margin: 10px;
}
input[type=text]{
  width: 100%;
  background-color: transparent;
  font-size: 20px;
  border: solid 3px #DACBB8;
  border-radius: 15px 0px 15px 0px;
}
input[type=text]:hover{
  width: 100%;
  background-color: transparent;
  font-size: 20px;
  border: solid 3px #eddcd2;
  border-radius: 0px 15px 0px 15px;
}
input:focus {
  outline: none;
}
input[type=submit]{

  border-style: dashed;
  width: 60px;
  height: 30px;
  color: black;
}
.save {
  position: relative;
  display: inline-block;
  border-bottom: 0px ;
  height: 30px;
}
.save:hover{
  opacity:80%
}



</style>
