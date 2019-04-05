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
background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 1000'%3E%3Cg %3E%3Ccircle fill='%23554b48' cx='50' cy='0' r='50'/%3E%3Cg fill='%235d524f' %3E%3Ccircle cx='0' cy='50' r='50'/%3E%3Ccircle cx='100' cy='50' r='50'/%3E%3C/g%3E%3Ccircle fill='%23655955' cx='50' cy='100' r='50'/%3E%3Cg fill='%236c605c' %3E%3Ccircle cx='0' cy='150' r='50'/%3E%3Ccircle cx='100' cy='150' r='50'/%3E%3C/g%3E%3Ccircle fill='%23756763' cx='50' cy='200' r='50'/%3E%3Cg fill='%237d6f6a' %3E%3Ccircle cx='0' cy='250' r='50'/%3E%3Ccircle cx='100' cy='250' r='50'/%3E%3C/g%3E%3Ccircle fill='%23857671' cx='50' cy='300' r='50'/%3E%3Cg fill='%238d7e78' %3E%3Ccircle cx='0' cy='350' r='50'/%3E%3Ccircle cx='100' cy='350' r='50'/%3E%3C/g%3E%3Ccircle fill='%2395857f' cx='50' cy='400' r='50'/%3E%3Cg fill='%239e8d86' %3E%3Ccircle cx='0' cy='450' r='50'/%3E%3Ccircle cx='100' cy='450' r='50'/%3E%3C/g%3E%3Ccircle fill='%23a6958d' cx='50' cy='500' r='50'/%3E%3Cg fill='%23af9d95' %3E%3Ccircle cx='0' cy='550' r='50'/%3E%3Ccircle cx='100' cy='550' r='50'/%3E%3C/g%3E%3Ccircle fill='%23b8a59c' cx='50' cy='600' r='50'/%3E%3Cg fill='%23c0ada4' %3E%3Ccircle cx='0' cy='650' r='50'/%3E%3Ccircle cx='100' cy='650' r='50'/%3E%3C/g%3E%3Ccircle fill='%23c9b5ab' cx='50' cy='700' r='50'/%3E%3Cg fill='%23d2bdb3' %3E%3Ccircle cx='0' cy='750' r='50'/%3E%3Ccircle cx='100' cy='750' r='50'/%3E%3C/g%3E%3Ccircle fill='%23dbc5ba' cx='50' cy='800' r='50'/%3E%3Cg fill='%23e4cec2' %3E%3Ccircle cx='0' cy='850' r='50'/%3E%3Ccircle cx='100' cy='850' r='50'/%3E%3C/g%3E%3Ccircle fill='%23edd6c9' cx='50' cy='900' r='50'/%3E%3Cg fill='%23f6ded1' %3E%3Ccircle cx='0' cy='950' r='50'/%3E%3Ccircle cx='100' cy='950' r='50'/%3E%3C/g%3E%3Ccircle fill='%23ffe7d9' cx='50' cy='1000' r='50'/%3E%3C/g%3E%3C/svg%3E");
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
