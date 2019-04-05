<template>
  <div id="app">
    <Calendar @selectDay="selectDay"/>
    <transition name = "slide-fade">
    <Details :day="selectedDay" v-if="selectedDay" @selectedSession="addSession" @quitSession="quitSession" @unselectDay="unselectDay"/>
    </transition>
    <Signups :signupList="sortedSignups"/>
  </div>
</template>

<script>
import Calendar from "./components/Calendar.vue";
import Details from "./components/DayDetails.vue";
import Signups from "./components/Signups.vue"

export default {
  name: "app",
  components: {
    Calendar,
    Details,
    Signups
  },
  data(){
    return{
      selectedDay:null,
      signUps:[]
    }
  },
  methods:{
    selectDay(day){
      this.selectedDay = day;
    },
    addSession(session){
      this.signUps.push(session)
    },
    unselectDay(){
      this.selectedDay = null;
    },
  quitSession(session){
   this.signUps = this.signUps.filter(signup =>{
     const same = (new Date(signup.date).getDay() === new Date(session.date).getDay() && signup.time === session.time && signup.name === session.name )
      return !same
     } ) 
  }
  },
  computed:{
    sortedSignups(){
      return this.signUps.sort(function(a,b){
  // Turn your strings into dates, and then subtract them
  // to get a value that is either negative, positive, or zero.
  return new Date(a.date) - new Date(b.date);
});
    }
  }
}
</script>

<style>
@import './assets/css/bootstrap.min.css';

body{
background-color: #554b48;
background-image: url("https://images.unsplash.com/photo-1476480862126-209bfaa8edc8?ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80");
background-attachment: fixed;
background-size: contain;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display:flex;
  justify-content: center;
  flex-wrap:wrap;
  /* background-color: #ffffff; */

}

/* Enter and leave animations can use different */
/* durations and timing functions.              */
.slide-fade-enter-active {
  transition: all .5s ease;
}
.slide-fade-leave-active {
  transition: all .4s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}

</style>
