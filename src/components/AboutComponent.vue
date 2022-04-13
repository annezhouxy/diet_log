<template>
  <div class="about">
    <h1>This is an about page</h1>
    <p>
    Welcome to the Diet Log App. Let's get started!
    </p>
    <div>
      <div v-if="diet_log.length"> 
        <DietLog  v-for = "log of diet_log" v-bind:key = "log.key" v-bind = "paragraph_attribute" v-bind:log = "log">{{log}}</DietLog>
     
      </div>
      <p v-else>Diet Log is empty.</p>
    </div>
     <button @click="addPlaceHolderLog">click to add place holder log</button>
     <button @click="diet_log.push({})">click to add an empty log</button>



  </div>
</template>

<style scoped>
p{
  color: grey;
  font-size: 30px
}
</style>

<script>
import DietLog from './DietLog.vue'
export default {
  components: { DietLog },
    data(){
        const log1 = {key:0, "date":"June 6,2021", "time":"5:00", "category":"meat", "name":"steak","weight":200, "caleries":200}
 
        const log2 = {key:1, "date":"June 8,2021", "time":"7:30", "category":"sweet", "name":"chocolate","weight":50, "caleries":250}
 
        const log3 = {key:2, "date":"May 10,2021", "time":"12:40", "category":"vegetable", "name":"carrot","weight":100, "caleries":80}
 
        const log4 = {key:3, "date":"July 6,2021", "time":"8:27", "category":"dairy", "name":"milk","weight":150, "caleries":150}
 
        const log5 = {key:4, "date":"December 12,2021", "time":"10:10", "category":"grain", "name":"oat","weight":30, "caleries":120}
        return {
            diet_log:[log1, log2, log3, log4, log5],
            paragraph_attribute: {
              style:{
                color: 'grey',
                backgroundColor: 'lightgrey'
              }
            }

        }

    
    },
    methods: {
      addPlaceHolderLog(){
        const placeHolderLog = {"date":"June 6,2021", "time":"5:00", "category":"meat", "name":"steak","weight":200, "caleries":200}
        this.diet_log.push(
          placeHolderLog
        )
      }
    }
}  
</script>
