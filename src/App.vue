<template>
  <div id="app">
    <h1>gestion de promotions</h1>
    <img class="kitten" src="./assets/chaton.jpg" alt="chaton">
    <h1>Liste des promotions</h1>
      <input type="text" placeholder="name" v-model="newName">
      <input type="date" placeholder="date début" v-model="newstartDate">
      <input type="date" placeholder="date fin" v-model="newendDate">
    <button v-on:click="createPromotion">create</button>
    <Promotion v-for="(promotion, index) in promotions" v-bind:promotion="promotion" v-bind:key="index"></Promotion>
   
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld'
import Promotion from "./components/Promotion";

export default {
  name: "App",
  components: {
    // HelloWorld
    Promotion
  },
  data() {
    return {
      promotions: []
    };
  },
  methods: {
    getPromotions: function() {
      fetch("http://api-students.popschool-lens.fr/api/promotions")
        .then(response => response.json())
        .then(response => {
          console.log("ok");
          this.promotions = response["hydra:member"];
        });
    },

    createPromotion: function() {

      fetch("http://api-students.popschool-lens.fr/api/promotions",{
       headers: {
           'Accept': 'application/json',
           'Content-Type': 'application/json'
       },
       // use the put method on the fetch to modify the existing string
       method: "POST",
       // change the value of the input newPromo field to Json string via stringify
       body: JSON.stringify({
           name: this.newName,
           startDate: this.newstartDate,
           endDate: this.newendDate

       })
    })

    }



  },

  mounted() {
    this.getPromotions();
  }
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

  color: #2c3e50;
  margin-top: 60px;
}

.kitten {
  width: 50%;
  box-shadow: 15px 25px 15px red;
}

h1 {
  color: red;
}
</style>
