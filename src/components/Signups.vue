<template>
    <div id="signups" v-bind:class="{'signupsClosed':!this.open, 'signupsOpen':this.open}">
        <b>
            <span @click="open=!open">
                Signups
            </span> 
        </b>
        <span v-if="!open" class = "signedUpNumber"> - {{signupList.length}}</span>
       <i> <p>Click to Toggle</p></i>
        <div v-if="open && signupList.length>0" class = "signupDetails container" >
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
    padding-bottom:1em;
    background-color:rgb(0,0,0,.5);
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
    min-height:200px;
    padding-top:1em;
}

.signupDetails{
    padding:1em;
    background-color:rgb(0,0,0,.8)
}

.signedUpNumber{
    font-size:20px;
}

</style>
