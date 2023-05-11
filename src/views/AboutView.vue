<template>
  <div class="about">
    <h1 v-bind = "title_attribute">Welcome to the Diet Log App! </h1>
    <p v-bind = "paragraph_attribute">
      You can start your journey here by tracking your calorie intake of the day. Please eat healthy and stay hydrated!</p>
  </div>
  
</template>

<style scoped>
h1{
    padding-top: 3%;
      color: rgb(164, 167, 171);
  font-size: 30px;
  line-height: 40px;
  font-family: 'Product Sans';

}
p{
  padding-top: 1.5%;
  color: rgb(115, 115, 115);
  font-size: 22px;
  line-height: 40px;
  font-family: 'Product Sans';
}

</style>

<script>
export default {
//   components: {
//   },
//   data(){
//     return{
//       title_attribute:{
//         style:{
//           color: 'grey'
//         }
//       },
//       paragraph_attribute:{
//         style:{
//           color: 'grey'
//         }
//       }

//     }
//   }
 }
</script>

