<template>
    <button id = 'day' 
        v-on:click="selectDay"
        class = "button button-success pb-4"
        v-bind:class="{'dayNoClasses':day.classes.length == 0}">
        <h4>
        {{day.date.getDate()}}
        </h4>
            {{day.classes.length}} {{classString}}<br>
           <span v-bind:class="{'signedUp':signedUp > 0}"> 
               {{signedUp}} signed up  
           </span>     
    </button>
</template>

<script>
export default {
    props:['day'],
methods:{
    selectDay(){
        if(this.day.classes.length > 0){
        this.$emit('selectedDay',this.day)
        }
    }
},
    computed:{
        classString(){
            return this.day.classes.length === 1 ? 'class' : 'classes'
        },
        signedUp(){
            return this.day.classes.filter(classObj => classObj.signedUp == true).length
        }
    }
}
</script>

<style scoped>

#day{
    /* background-color:burlywood; */
    width:100px;
    height:100px;
    display:flex;
    /* align-items: center; */
    justify-content: center;
    flex-direction: column;
    align-items: center;
    align-content: center;
    transition:.3s;
    border-radius: 10px;
    background-color:lightcyan;
    font-size:12px;
}
#day:hover{
    background-color:lightblue;
}

.dayNoClasses{
    background-color:lightgrey !important;
}

.dayNoClasses:active{
    background-color:red !important;
}

h4{
    padding:0;
    margin:0;
}

.signedUp{
    color:green;
    font-size:12px;
}
</style>

