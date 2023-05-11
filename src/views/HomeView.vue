<template>
  <div class="about">
    <p class = "welcome">Welcome to the Diet Log App. Here is your log!</p>
    <div class = "card">
      <md-table md-card >
        <md-table-toolbar>
          <h1 class="md-title">User Name</h1>
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
    <br><br><br>
    <button @click="addPlaceHolderLog">click to add place holder log</button>
    <button @click="dietLogs.push({})">click to add an empty log</button>
  </div>
</template>

<style scoped>
.welcome{
  font-size: 27px;
  padding-top: 1.1%;
  font-family: 'Product Sans';
}
.card{
    padding-top: 1.1%;
}

</style>
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