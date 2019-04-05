<template>
    <div id="signups" v-bind:class="{'signupsClosed':!this.open, 'signupsOpen':this.open}">
        <b>
            <span @click="open=!open">
                Signups
            </span> 
        </b>
        <span v-if="!open" class = "signedUpNumber"> - {{signupList.length}}</span>
       <i> <p>Click to Toggle</p></i>
        <div v-if="open" class = "signupDetails" >
            <div v-for="signup in signupList" :key="signup.name+signup.date">
                {{signup.date.getMonth()+1+"/" + signup.date.getDate() }} - {{signup.name}} - {{signup.time+":00"}}
            </div>
        </div>
    </div>
</template>

<script>
export default {   
    props:['signupList'],
data(){
    return{
        open:false
    }
}
}
</script>

<style>
#signups{
    width:400px;
    padding-bottom:2em;
    background-color:gray;
    position: fixed;
    color:white;
    bottom: 0;
    right: 0;
    border-radius:25px 25px 0 0;
    transition:1s;
  }

.signupsClosed{
    cursor:pointer;
}
.signupsOpen{
    height:400px;
    padding-top:1em;
}

.signupDetails{
    padding:1em;
}

.signedUpNumber{
    font-size:20px;
}

</style>
