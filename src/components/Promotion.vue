<template>
  <div class="promotion">
    <h1>{{ promotion.name }}</h1>
    <h1>Date de début = {{ promotion.startDate }}</h1>
    <h1>Date de fin = {{ promotion.endDate }}</h1>
    <input type="text" v-model="promotion.name">
    <button v-on:click="updatePromotion">update</button>
      <button v-on:click="deletePromotion">delete</button>
    <Student v-for="(studentURL, index) in promotion.students" v-bind:myURL="studentURL" v-bind:key="index">
   
    </Student>
    <!-- <ul class= "studentlist">
      <li v-for="studentURL in promotion.students" class="studentitems">
        {{ studentURL }}
      </li>
    </ul> -->
  </div>
</template>

<script>
import Student from "./Student";

export default {
  name: 'Promotion',
  components: {
    // HelloWorld
    Student,
  },
  props: {
    promotion: Object
  },
  
  methods: {
   updatePromotion(event){
     console.log(this.promotion.name + "updated");
     fetch("http://api-students.popschool-lens.fr" + this.promotion['@id'],{
       headers: {
           'Accept': 'application/json',
           'Content-Type': 'application/json'
       },
       // use the put method on the fetch to modify the existing string
       method: "PUT",
       // change the value of the input newPromo field to Json string via stringify
       body: JSON.stringify({
           name: this.promotion.name
       })
    })
  },

   deletePromotion(event){
     console.log(this.promotion.name + "deleted")
      fetch("http://api-students.popschool-lens.fr" + this.promotion['@id'],{
       method: "DELETE",
      
    })
   }
  },
 
};
</script>

<style scoped>
.promotion {
  width: 100%;
  height: 25%;
  background-color: black;
}

h1 {
  color: white;
}

li {
color: white;
}

.studentlist{
  display: flex;
  flex-flow: row wrap;
  margin: 10px 50px; padding: 15px 5px;
  background-color: navajowhite;
}

.studentitems{
  display: block;
  background-color: #aa44ff;
  margin: 10px 50px; padding: 15px 5px;
}


</style>

