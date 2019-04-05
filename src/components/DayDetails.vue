<template>
    <div id = "day-details" class="pt-3">
        <div class = "row">
            <div class = "col-sm-10"></div>
            <div class = "col-sm-2">
        <h2 @click="unselectDay">X</h2>
            </div>
        </div>
        <div v-if="day">
            <h2>
        {{month}} {{numericDay}}
        </h2>
        <div v-for="session in day.classes" :key="session.id + session.date">
            <Details :session="session" :day="day" @selectedSession="selectSession" @quitSession="quitSession"/>
            </div>
        </div>
    </div>
</template>

<script>
import Details from "./ClassDetails"

export default {
props:["day"],
components:{
    Details
},
computed:{
    month(){
        return new Date(this.day.date).getMonth() == "3" ? "April":"May"
    },
    numericDay(){
        return new Date(this.day.date).getDate()
    }
},
methods:{
    selectSession(e){
        this.$emit('selectedSession',e)
    },
    unselectDay(){
        this.$emit('unselectDay')
    },
    quitSession(session){
        this.$emit('quitSession',session)
    }
},
created(){
}
}
</script>
<style>
#day-details{
    min-width:300px;
    min-height:80vh;
    border-radius:25px;
    margin-left:2em;
    background-color:ivory;
}
</style>
