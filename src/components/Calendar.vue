<template>
<div class = "calendarWrapper">
    <h3>Class Calendar for Healthy Living </h3>
    <h4>April</h4>
    <div id = "calendar">
        <Day 
        v-for="day in dates" 
        :key="day.key" 
        :day="day"
        @selectedDay ="selectDay"/>
    </div>
</div>
</template>

<script>
import Day from "./Day"
export default {
    components:{
        Day
    },
    data(){
    return{
      dates:[],
      classes:[
          {
              id:1,
              name:"Kickboxing with Kelly",
              time:17
          },
          {
              id:2,
              name:"Sunrise Yoga with Martha",
              time:7
          },
          {
              id:3,
              name:"Spin with Jorge",
             time:12,
          },
          {
          id:4,
          name:'Tae Kwon Do with Tai Kwon',
          time:16,
          },
          {
          id:5,
          name:'Evening Yoga with Roselle',
          time:19,
          },

          {
          id:6,
          name:'Thai Chi with Charles',
          time:8,
          },

      ]
    }
  },
  methods:{
      getDates(){
        for(let i = 1; i <36;i++){
        const date = i < 31 ? new Date(`2019-4-${i}`) : new Date(`2019-5-${i-30}`)
        this.dates.push({date:date,classes:this.addClass(),key:i})
        }
        },
        addClass(){
            const classList = []
            const randInt = Math.floor(Math.random()*4)
            for(var i = 0;i<randInt;i++){
                const randClass = this.classes[Math.floor(Math.random()*this.classes.length)];
                classList.push({session:randClass,signedUp:false})
            }
            return classList
        },
        selectDay(day){
            this.$emit("selectDay", day)
        }
      },
  created(){
      this.getDates()
  }
};

</script>

<style>

#calendar{
    display:flex;
    flex-wrap: wrap;
    max-width:700px;
}

.calendarWrapper{
    background-color:rgb(255,255,255,.6);
    padding:1em;
    margin-left:1em;
    border-radius:25px;
}

</style>
