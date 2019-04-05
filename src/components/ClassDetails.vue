<template>
    <div class = "class-details" v-bind:class="{ 'class-details-selected': this.session.signedUp, 'class-details':!this.session.signedUp }" >
       <h4> {{session.session.name}} </h4> <p>at {{session.session.time+":00"}}</p>
        <br/>
        <button v-if="!session.signedUp" @click="signUpForClass(session)">Sign up!</button>
        <button v-if="session.signedUp" @click="quitSession(session)">Unregister :-(</button>
        
        </div>
</template>

<script>
export default {
props:['session','day']
,
methods:{
    signUpForClass(session){
        session.signedUp = true;
       const sessionSignup = {
            name:session.session.name,
            date : this.day.date,
            time: session.session.time
            }
            this.$emit('selectedSession',sessionSignup)
    },
    quitSession(session){
        session.signedUp = false;
          const sessionSignup = {
            name:session.session.name,
            date : this.day.date,
            time: session.session.time
            }
        this.$emit('quitSession',sessionSignup)
    }
}
}
</script>

<style>
.class-details{
    background-color:lightcoral;
    margin-right:4em;
    margin-left:4em;
    padding:3em;
    border-radius:20px;
}
.class-details-selected{
    background-color:greenyellow;
}
</style>
