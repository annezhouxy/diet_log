<template>
  <div class="about">
    <p>Welcome to the Diet Log App. Let's get started!</p>
    <!-- <div>
      <table v-if="dietLogs.length"> 
       <tr>   
          <th>Date</th>
          <th>Time</th>
          <th>Category</th>
          <th>Name</th>
          <th>Weight</th>
          <th>Calories</th>
        </tr>
        <DietLog  v-for = "log of dietLogs" v-bind:key = "log.key" v-bind:log = "log">{{log}}
        </DietLog>

     
      </table>
      <p v-else>Diet Log is empty.</p>
    </div> -->
    <div>
      <md-table md-card>
        <md-table-toolbar>
          <h1 class="md-title">Users</h1>
        </md-table-toolbar>

        <md-table-row>
          <md-table-head>Date</md-table-head>
          <md-table-head>Time</md-table-head>
          <md-table-head>Category</md-table-head>
          <md-table-head>Name</md-table-head>
          <md-table-head>Weight</md-table-head>
          <md-table-head>Calories</md-table-head>
        </md-table-row>
        <DietLog v-for="log of dietLogs" v-bind:key="log.key" v-bind:log="log"
          >{{ log }}
        </DietLog>
      </md-table>
    </div>
    <button @click="addPlaceHolderLog">click to add place holder log</button>
    <button @click="dietLogs.push({})">click to add an empty log</button>
  </div>
</template>

<script>
import DietLog from "@/components/DietLog.vue";
export default {
  components: { DietLog },
  created() {
    console.log(this.dietLogs);
    const serverURL = 
      process.env.NODE_ENV === "production"
      ? "https://3vkc0vullg.execute-api.us-east-2.amazonaws.com/dev"
      : "http://localhost:3000"
      fetch(serverURL+"/dietLogs", {
      method: "GET",
      mode: "cors",
      headers: {
        "Content-Type": "application/json",
        // "Access-Control-Allow-Origin": "*",
        Accept: "*/*",
      },
    })
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.dietLogs.push(...data);
      })
      .catch((err) => {
        console.log(err);
      });
  },
  data() {
    return {
      dietLogs: [],
      paragraph_attribute: {
        style: {
          color: "grey",
          backgroundColor: "lightgrey",
        },
      },
    };
  },
  methods: {
    addPlaceHolderLog() {
      const placeHolderLog = {
        date: "June 6,2021",
        time: "5:00",
        category: "meat",
        name: "steak",
        weight: 200,
        calories: 200,
      };
      this.dietLogs.push(placeHolderLog);
    },
  },
};
</script>